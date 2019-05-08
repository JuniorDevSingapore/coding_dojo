# Python - Bootstrapping pytest Test Suite

*__Note__: This guide assumes you have Python installed.*

1. Install [pipenv]

   ```shell
   pip install pipenv
   ```

2. Create a new project folder for the code:

   (*Assuming the project is named `new_kata`*)
   
   ```shell
   mkdir new_kata
   cd new_kata
   ```
   
3. In the new project folder, install pytest as a development dependency

   ```shell
   pipenv install --dev pytest
   ```
   
4. Create a test file (`test_sum.py`) with the following content:

   ```python
   from sum import sum
   
   
   class TestSum:
       def test_additions_are_additive(self):
           assert sum(1, 1)  == 2, "expected two numbers to add up"
   ```
   
4. Create `sum.py` with the following content:

   ```python
   def sum(a, b):
       return a + b
   ```

5. Run the test:

  ```shell
  pipenv run pytest
  ```
  
  You should see this:
  
  ```shell
  === test session starts ===
  platform darwin -- Python 3.6.1, pytest-4.4.1, py-1.8.0, pluggy-0.11.0
  rootdir: /Users/ba/workspace/coding_dojo
  collected 1 item

  test_sum.py .             [100%]

  === 1 passed in 0.02 seconds ===
  ```

## About pytest

Pytest is a fairly magic library that extends Python's built-in `assert` to
handle most types in a nice understandable way. For instance, if you ask it to
compare two lists it'll happily tell you which of the two lists contains a
differing item and where it is. For example:

```python
def test_failing_lists(self):
    assert [1] == [1, 2]
```

will give you the following output:

```shell
=== test session starts ===
platform darwin -- Python 3.6.1, pytest-4.4.1, py-1.8.0, pluggy-0.11.0
rootdir: /Users/ba/workspace/coding_dojo
collected 2 items

test_sum.py .F [100%]

=== FAILURES ===
___ TestSum.test_failing_lists ___

self = <test_sum.TestSum object at 0x10205c8d0>

    def test_failing_lists(self):
>       assert [1] == [1, 2]
E       assert [1] == [1, 2]
E         Right contains more items, first extra item: 2
E         Use -v to get the full diff

test_sum.py:9: AssertionError
=== 1 failed, 1 passed in 0.06 seconds ===
```

## About pipenv

Pipenv is a tool for managing all your dependencies and helping you make sure
the correct version of them is installed everywhere (it's similar to Ruby's
`bundler`). It will under the hood create a [virtual environment
(venv/virtualenv)] for you and keep all of your current project's dependencies
separate from any other app. To learn more about pipenv check out the
[website][pipenv].

[pipenv]: https://pipenv.readthedocs.io/en/latest/
[virtualenv]: https://virtualenv.pypa.io/en/stable/
