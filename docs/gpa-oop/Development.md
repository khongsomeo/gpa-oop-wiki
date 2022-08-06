# Testing
## Guide
Adding a new test case named `19120338`:
- Payload: write test payloads to `tests/input/19120338.inp`
- Output: write expected output to `tests/output/19120338.out`

Running tests:
1. `make`
2. `make init_test`
3. `make test` (or silent mode: `make test_silent` - without progress bar)

## Inside the tests
- For step 1: `Makefile` will compile a new binary.
- For step 2: `Makefile` will copy that new binary to the `tests/` folder.
- For step 3: The test module `tests/test.pl` will be triggered: first it read the input inside `tests/input/<testname>.inp` then compare with the output inside `tests/output/<testname>.out`. This will run until all test cases are checked and any failed case will break the procedure immediately.

# Test coverage
We support code coverage reports! Just make sure you have `lcov` installed.
1. `make gcov`
2. `make init_test`
3. `make test`
4. `make lcov`
5. `make generate-coverage-report`

Coverage Report will be automatically generated inside `coverage/`


# Format
We require your code to be formatted with `clang-format` before going further.
Follow these steps:

Install `clang-format`:
```
sudo apt-get install clang-format
```

Run checks:
```
make lint
```

If there are any linting errors, run `make format` to format it.
```
make format
```

# Junk hunter
As described in `jh.pl`, this file checks if any binary or coverage reports are mistakenly visible to Git. This prevents pushing garbage to the remote.
