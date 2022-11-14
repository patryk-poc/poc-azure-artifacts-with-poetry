# poc-azure-artifact-release

[![Build Status](https://dev.azure.com/kpatryk/Playground/_apis/build/status/patryk-poc/test-azure-pipeline?branchName=feature%2Fcheck-azure-artifacts-release-procedure)](https://dev.azure.com/kpatryk/Playground/_build/latest?definitionId=1&branchName=feature%2Fcheck-azure-artifacts-release-procedure)
[![codecov](https://codecov.io/gh/patryk-poc/test-azure-pipeline/branch/feature/check-azure-artifacts-release-procedure/graph/badge.svg?token=LDED35KG6U)](https://codecov.io/gh/patryk-poc/test-azure-pipeline)
[![Commit activity](https://img.shields.io/github/commit-activity/m/patryk-poc/test-azure-pipeline)](https://img.shields.io/github/commit-activity/m/patryk-poc/test-azure-pipeline)
[![Code style with black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Imports with isort](https://img.shields.io/badge/%20imports-isort-%231674b1)](https://pycqa.github.io/isort/)
[![License](https://img.shields.io/github/license/patryk-poc/test-azure-pipeline)](https://img.shields.io/github/license/patryk-poc/test-azure-pipeline)

This is a template repository for Python projects that use Poetry for their dependency management.

- **Github repository**: <https://github.com/patryk-poc/test-azure-pipeline/>
<!-- - **Documentation** <https://kpatryk.github.io/test-azure-pipeline/> -->

## Getting started with your project

Clone the repository:

``` bash
git clone git@github.com:patryk-poc/test-azure-pipeline.git
cd test-azure-pipeline/poc-azure-artifact-release
```

Finally, install the environment and the pre-commit hooks with

```bash
make install
```

You are now ready to start development on your project! The CI/CD
pipeline will be triggered when you open a pull request, merge to main,
or when you create a new release.

If you want to set-up for publishing to PyPi or Artifactory, see
[here](https://fpgmaas.github.io/cookiecutter-poetry/features/publishing/#set-up-for-pypi).
Currently publishing was enabled to Azure Artifacts feed.
For activating the automatic documentation with MkDocs, see
[here](https://fpgmaas.github.io/cookiecutter-poetry/features/mkdocs/#enabling-the-documentation-on-github).
To enable the code coverage reports, see [here](https://fpgmaas.github.io/cookiecutter-poetry/features/codecov/).

## Releasing a new version

The project uses `Azure Artifacts` feed to store packages and `twine` to publish it.
One of the dependency `artifacts-keyring` package is layered on top of our Azure Artifacts Credential Provider.
For more advanced configuration options, check out the [artifacts-credprovider](https://github.com/microsoft/artifacts-credprovider)

Create [Personal access token](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows#create-a-pat)
with `Packaging` > `Read` and `Write` scope to authenticate into Azure DevOps and to be able both to retrieve and publish packages.

You can also check out the following article [Publish and consume Python packages from the command line](https://learn.microsoft.com/en-us/azure/devops/artifacts/quickstarts/python-cli?view=azure-devops)

In order to publish a package to remote repository add the following section in your local `$HOME/.pypirc` file:


    [distutils]
    Index-servers =
        kpatryk

    [kpatryk]
    Repository = https://pkgs.dev.azure.com/kpatryk/_packaging/kpatryk/pypi/upload/
    Username = <PERSONAL_ACCESS_TOKEN>


In case the following error is returned when trying to publish a package to `Azure Artifact` feed:
`Exception: Unable to find dependency dotnet, please manually install the .NET SDK and ensure 'dotnet' is in your PATH.`
it can be resolved by installing a `dotnet` package, for example `brew install dotnet` on Mac.


The project version is configured inside `pyproject.toml` config in `[tool.poetry]` section, under `version` label.
In order to bump a version use `poetry version` command.

---

Repository initiated with [fpgmaas/cookiecutter-poetry](https://github.com/fpgmaas/cookiecutter-poetry).
