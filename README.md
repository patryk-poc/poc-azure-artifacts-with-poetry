# test-azure-artifacts-with-poetry

POC to create a Python package with poetry and set up Azure Pipeline to publish a newly built package into Azure Artifacts project-scoped feed. 

In order to publish a new package `version` attribute in `pyproject.toml`, under section `[tool.poetry]` need to be bumped, else it will be skipped from publishing. 

[Package documentation](poc-azure-artifact-release/README.md)
