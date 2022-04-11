Just a miscellaneous collection of [pre-commit][] hooks.

- **pip-compile** simply runs `pip-compile` before every commit.
  - **Why?** This makes sure no one you didn’t 1. forget to run `pip-compile`, 2. modify `requirements.txt` without modifying `requirements.in` 3. forget to stage either 4. have inconsistent `requirements.txt` and `requirements.in` for any reason.
  - **N.B.:** Make sure you whenever pre-commit is running this hook that the right Python virtual environment (if you are using one) is activated, and has `pip-tools` installed, so the hook can find the `pip-compile` executable.
  
[pre-commit]: https://pre-commit.com/
[pip-tools]: https://github.com/jazzband/pip-tools
