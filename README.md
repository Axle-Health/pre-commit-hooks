Collection of [pre-commit][] hooks.

- **pip-compile** simply runs `pip-compile` before every commit.
  - **Why?** This makes sure no one you didn’t 1. forget to run `pip-compile` after modifying `requirements.in`, 2. directly modify `requirements.txt` without modifying `requirements.in`, 3. forget to stage either in Git, 4. have inconsistent `requirements.txt` and `requirements.in` for any reason.
  - **Out-of-scope:** It won’t run `pip-sync` for you or make sure your environment is synced. You have control over that.
  - **N.B.** Make sure when pre-commit is running that the right Python virtual is activated if applicable and [pip-tools][] is installed, so the hook can find the right `pip-compile` executable. Otherwise, the hook will fail.


- **pip-compile-multi** is the same but for multiple `requirements.in` files.
  - **How it works:** It runs `pip-compile` for every file named `*requirements.in` in the root directory.
  - **Out-of-scope:** This won’t  work for requirements file ignored by Git. They must be staged for pre-commit to notice the `.in` and `.txt` files have fallen out of sync and block the commit.
  - **N.B.:** same as for `pip-compile`.
  
 
- **make-migrations** makes sure Django migration files have been created.
  - **How it works:** It runs `python manage.py makemigrations --check --dry-run` to make sure no migrations are left to be created.
  - **Out-of-scope:** It won’t make the migrations for you. If the hook fails, run `python manage.py migrations`, stage the migration files, and try committing again. 
  - **Out-of-scope:** It won’t run `python manage.py migrate` for you or check that migrations have been applied.  You have control over that.
  - **N.B.:** Make sure when the pre-commit is running that the right Python virtual environment is activated if applicable and there is a Django `manage.py` file you can run. Else, the hook will fail.
  
---

You can try out hooks in this repo without installing them by running
```bash
pre-commit try-repo https://github.com/Axle-Health/pre-commit-hooks
```

To install a pre-commit hook from this repo, simply add something like
```yaml
  - repo: https://github.com/Axle-Health/pre-commit-hooks
    rev: 1.1.0
    hooks:
      - id: pip-compile
      - id: make-migrations
```
to your `.pre-commit-config.yaml` file. Or if you don’t have one already, install [pre-commit][] first 

[pre-commit]: https://pre-commit.com/
[pip-tools]: https://github.com/jazzband/pip-tools_
