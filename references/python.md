# Python Project Templates

## pyproject.toml (Modern Python)

```toml
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "my-package"
version = "1.0.0"
description = "A brief description"
readme = "README.md"
requires-python = ">=3.9"
license = {text = "MIT"}
authors = [
    {name = "Name", email = "email@example.com"}
]
keywords = ["tag1", "tag2"]
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
]
dependencies = [
    "requests>=2.28.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.0",
    "black",
    "ruff",
    "mypy",
]

[project.scripts]
my-cli = "my_package.cli:main"

[tool.setuptools.packages.find]
where = ["src"]

[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py"]

[tool.black]
line-length = 100
target-version = ["py39", "py310", "py311"]

[tool.ruff]
line-length = 100
select = ["E", "F", "W", "I", "N"]

[tool.mypy]
python_version = "3.9"
warn_return_any = true
warn_unused_configs = true
```

## setup.py (Legacy)

```python
from setuptools import setup, find_packages

setup(
    name="my-package",
    version="1.0.0",
    description="A brief description",
    packages=find_packages(where="src"),
    package_dir={"": "src"},
    python_requires=">=3.9",
    install_requires=["requests>=2.28.0"],
    extras_require={
        "dev": ["pytest>=7.0", "black", "ruff"]
    },
)
```

## CI Workflow for Python

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ["3.9", "3.10", "3.11", "3.12"]
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
          cache: 'pip'
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -e ".[dev]"
      - name: Lint with ruff
        run: ruff check .
      - name: Type check with mypy
        run: mypy src
      - name: Test with pytest
        run: pytest --cov=src

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.11"
      - name: Build package
        run: |
          pip install build
          python -m build
      - name: Check package
        run: |
          pip install twine
          python -m twine check dist/*
```

## pytest Configuration

```ini
[pytest]
testpaths = tests
python_files = test_*.py
python_classes = Test*
python_functions = test_*
addopts = -v --strict-markers
markers =
    slow: marks tests as slow
    integration: marks tests as integration tests

[coverage:run]
source = src
omit =
    */tests/*
    */test_*.py

[coverage:report]
exclude_lines =
    pragma: no cover
    def __repr__
    raise AssertionError
    raise NotImplementedError
```

## Makefile

```makefile
.PHONY: install test lint format clean

install:
	pip install -e ".[dev]"

test:
	pytest

lint:
	ruff check .
	mypy src

format:
	black .
	isort .

clean:
	rm -rf build/ dist/ *.egg-info
	find . -type d -name __pycache__ -exec rm -rf +
	find . -type f -name "*.pyc" -delete
```

## Common Dependencies

| Category | Dependencies |
|----------|-------------|
| HTTP | requests, httpx |
| CLI | click, typer |
| Data | pandas, numpy |
| Testing | pytest, pytest-cov, pytest-mock |
| Linting | ruff, black |
| Type Checking | mypy, pyright |
| Serialization | pydantic, marshmallow |

## Package Structure

```
my-package/
├── src/
│   └── my_package/
│       ├── __init__.py
│       ├── module.py
│       └── cli.py
├── tests/
│   ├── __init__.py
│   └── test_module.py
├── pyproject.toml
├── README.md
├── LICENSE
└── .gitignore
```
