# Poetry and *flat* or *src* structure

* As of version `2.1.2` of `poetry`.
* We will use `poetry new` to create new projects.
* Compare the structure and code of a `flat` vs. `./src` layouts.

**References**

* [src layout vs flat layout](https://packaging.python.org/en/latest/discussions/src-layout-vs-flat-layout/)
* [Motivation due to Ruff](https://docs.astral.sh/ruff/faq/#how-does-ruff-determine-which-of-my-imports-are-first-party-third-party-etc)


## `./src` case

### Create the project

Since version [`2.1.0`](https://github.com/python-poetry/poetry/blob/main/CHANGELOG.md#210---2025-02-15) new projects default to the `/src` layout.
Run the following inside [`./de_code/src_layout/`](./de_code/src_layout/)

```bash
poetry new my_pkg
```

Next, in [`./de_code/src_layout/my_pkg`](./de_code/src_layout/my_pkg) run:

```bash
poetry add --group dev pytest
```

### Bring in the code

```python
# src_layout/my_pkg/src/my_pkg/my_module.py
def my_func():
    return 42
```

and

```python
# src_layout/my_pkg/tests/test_my_module.py
from my_pkg.my_module import my_func

def test_my_func():
    assert my_func() == 42
```

### Run tests

In `src_layout/my_pkg ` run:

```bash
poetry install
poetry run pytest
```

## Flat case

### Create the project

```bash
poetry new --flat my_pkg
```

Next, in [`./de_code/flat_layout/my_pkg`](./de_code/flat_layout/my_pkg) run:

```bash
poetry add --group dev pytest
```

### Bring in the code

```python
# flat_layout/my_pkg/my_pkg/my_module.py
def my_func():
    return 42
```

and

```python
# flat_layout/my_pkg/tests/test_my_module.py
from my_pkg.my_module import my_func

def test_my_func():
    assert my_func() == 42
```

### Run tests

In `src_layout/my_pkg ` run:

```bash
poetry install
poetry run pytest
```

## Let's compare

```bash
# Run from `./de_code`
diff flat_layout/my_pkg/pyproject.toml src_layout/my_pkg/pyproject.toml
```
