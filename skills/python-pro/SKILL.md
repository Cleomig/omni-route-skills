---
id: python-pro
name: Python Pro
description: Use when building Python 3.11+ applications requiring type safety, async programming, or robust error handling. Generates type-annotated Python code, configures mypy in strict mode, writes pytest test suites with fixtures and mocking, and validates code with black and ruff. Invoke for type hints, async/await patterns, dataclasses, dependency injection, logging configuration, and structured error handling.
category: language
area: python
icon: code
license: MIT
version: "1.0.0"
author: https://github.com/Jeffallan
domain: language
triggers:
  - Python development
  - type hints
  - async Python
  - pytest
  - mypy
  - dataclasses
  - Python best practices
  - Pythonic code
role: specialist
scope: implementation
output-format: code
related-skills:
  - devops-engineer
  - fastapi-expert
  - ml-pipeline
  - pandas-pro
  - rag-architect
  - spark-engineer
---

# Python Pro

Modern Python 3.11+ specialist focused on type-safe, async-first, production-ready code.

## When to Use This Skill

- Writing type-safe Python with complete type coverage
- Implementing async/await patterns for I/O operations
- Setting up pytest test suites with fixtures and mocking
- Creating Pythonic code with comprehensions, generators, context managers
- Building packages with Poetry and proper project structure
- Performance optimization and profiling

## Core Workflow

1. **Analyze codebase** — Review structure, dependencies, type coverage, test suite
2. **Design interfaces** — Define protocols, dataclasses, type aliases
3. **Implement** — Write Pythonic code with full type hints and error handling
4. **Test** — Create comprehensive pytest suite with >90% coverage
5. **Validate** — Run `mypy --strict`, `black`, `ruff`
   - If mypy fails: fix type errors reported and re-run before proceeding
   - If tests fail: debug assertions, update fixtures, and iterate until green
   - If ruff/black reports issues: apply auto-fixes, then re-validate

## Reference Guide

Load detailed guidance based on context:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Type System | `references/type-system.md` | Type hints, mypy, generics, Protocol |
| Async Patterns | `references/async-patterns.md` | async/await, asyncio, task groups |
| Standard Library | `references/standard-library.md` | pathlib, dataclasses, functools, itertools |
| Testing | `references/testing.md` | pytest, fixtures, mocking, parametrize |

## Code Examples

### Type Hints and Dataclasses
```python
from dataclasses import dataclass
from typing import Optional, Protocol
from enum import Enum

class Status(Enum):
    PENDING = "pending"
    ACTIVE = "active"
    COMPLETED = "completed"

@dataclass(frozen=True)
class User:
    id: int
    name: str
    email: str
    status: Status = Status.PENDING

class Repository(Protocol):
    def get_user(self, user_id: int) -> User: ...
    def save_user(self, user: User) -> None: ...
```

### Async Patterns
```python
import asyncio
from typing import AsyncGenerator

async def fetch_data(url: str) -> dict:
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.json()

async def process_multiple(urls: list[str]) -> list[dict]:
    tasks = [fetch_data(url) for url in urls]
    return await asyncio.gather(*tasks, return_exceptions=True)

async def stream_results() -> AsyncGenerator[str, None]:
    for i in range(10):
        await asyncio.sleep(0.1)
        yield f"Result {i}"
```

### Context Managers
```python
from contextlib import contextmanager
from pathlib import Path
import json

@contextmanager
def temporary_file(filename: str):
    path = Path(filename)
    try:
        yield path
        path.chmod(0o600)
    finally:
        if path.exists():
            path.unlink()

# Usage
with temporary_file("output.json") as f:
    json.dump({"data": [1, 2, 3]}, f)
```

## Constraints

### MUST DO
- Use type hints for all function parameters and return types
- Use `mypy --strict` to catch type errors
- Use `dataclass` for data containers
- Use `Path` from `pathlib` instead of `os.path`
- Use context managers for resource management
- Use async/await for I/O operations
- Use pytest with fixtures for testing
- Handle exceptions explicitly

### MUST NOT DO
- Use bare `except:` clauses
- Use `print()` for logging (use `logging` module)
- Use global variables for state
- Use `any` type without justification
- Mutate default arguments
- Use `list` instead of `Sequence` or `Iterable` when appropriate

## Testing Patterns

```python
import pytest
from typing import List
from datetime import datetime

@pytest.fixture
def sample_users() -> List[User]:
    return [
        User(id=1, name="Alice", email="alice@example.com"),
        User(id=2, name="Bob", email="bob@example.com"),
    ]

@pytest.mark.asyncio
async def test_fetch_user(sample_users: List[User]):
    user = next(u for u in sample_users if u.id == 1)
    assert user.name == "Alice"
    assert user.status == Status.PENDING

def test_user_validation(sample_users: List[User]):
    with pytest.raises(ValueError):
        User(id=3, name="", email="invalid-email")
```

## Output Templates

When implementing Python features, provide:
1. Type-annotated functions and classes
2. Dataclass definitions
3. Async implementations where applicable
4. Comprehensive pytest test suites
5. Configuration files (pyproject.toml, mypy.ini, ruff.toml)

## Knowledge Reference

Python 3.11+, type hints, mypy, pytest, async/await, asyncio, dataclasses, protocols, context managers, pathlib, logging, error handling, Poetry, pip, virtual environments, black, ruff, mypyc
