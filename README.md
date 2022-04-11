Just a miscellaneous collection of [pre-commit][] hooks.

- **pip-compile** simply runs `pip-compile` before every commit.
  - **Why?** This makes sure no one you didn’t 1. forget to run `pip-compile`, 2. modify `requirements.txt` without modifying `requirements.in` 3. forget to stage either 4. have inconsistent `requirements.txt` and `requirements.in` for any reason.
  - **N.B.:** Make sure you whenever pre-commit is running this hook that the right Python virtual environment (if you are using one) is activated, and has `pip-tools` installed, so the hook can find the `pip-compile` executable.
  - **Edge cases:** If the hook doesn’t find the `pip-compile` executable in its path, it will fail, which is just as well. It’s possible it might find a version of `pip-compile` installed with a different Python version than you intended and mess up things, but in any case, it will be useful to flag that some change might need to happen.  
  
---

To use a pre-commit hook from this repo, simply add something like:
```yaml
  - repo: https://github.com/Axle-Health/pre-commit-hooks
    rev: c4e351bd7cfe61a7f5685596acf6768ccf892346
    hooks:
      - id: pip-compile
```
to your existing `.pre-commit-config.yaml` file. 

You can also try out hooks in this repo without installing it first by running `pre-commit try-repo https://github.com/yatharth/pre-commit-hooks`.


[pre-commit]: https://pre-commit.com/
[pip-tools]: https://github.com/jazzband/pip-tools
