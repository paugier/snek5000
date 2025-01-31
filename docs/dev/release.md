# Release checklist for maintainers

## Via GitHub Actions

- Update {ref}`changelog/unreleased` with version comparison links and detailed
  description.
- Update version and date in `CITATION.cff`.
- Make a [new release] on Github.
- Inspect upload in [TestPyPI].
- Execute manual [deploy workflow] to download from [TestPyPI], run tests and publish to
  [PyPI].

## Manual method (not recommended)

```{note}
For demonstration's sake, we assume that the next version is `$VERSION`.
```

- Install nox:

  ```
  pip install nox
  ```

- Ensure tests pass locally and on CI:

  ```
  nox -s tests
  ```

- Compile documentation:

  ```
  nox -s docs
  ```

- Commit changes and make an annotated tag:

  ```
  git commit
  git tag -a $VERSION
  ```

- Build and upload to [TestPyPI]:

  ```
  nox -s testpypi
  ```

- Download, test and upload to [PyPI]:

  ```
  nox -s pypi
  ```

- Upload to repository:

  ```
  git push --follow-tags --atomic origin main
  ```

[deploy workflow]: https://github.com/snek5000/snek5000/actions/workflows/deploy.yaml
[new release]: https://github.com/snek5000/snek5000/releases/new
[pypi]: https://pypi.org/project/snek5000/
[testpypi]: https://test.pypi.org/project/snek5000/
