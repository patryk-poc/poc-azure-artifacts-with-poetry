
disable-hooks:
	@git config --global --unset core.hooksPath || true

install-twine: ## Install only tools required to build & publish to Azure Artifacts
	@poetry install --only=artifacts

install: disable-hooks install-twine ## Install the poetry environment and install the pre-commit hooks
	@echo "🚀 Creating virtual environment using pyenv and poetry"
	@poetry install
	@poetry run pip install -U pip wheel setuptools
	@poetry run pre-commit install

check: ## Lint and check code by running black, isort, flake8, mypy and deptry.
	@echo "🚀 Checking Poetry lock file consistency with 'pyproject.toml': Running poetry lock --check"
	@poetry lock --check
	@echo "🚀 Show outdated project packages"
	@poetry run pip list --outdated
	@echo "🚀 Linting code: Running pre-commit"
	@poetry run pre-commit run -a
	@echo "🚀 Checking code formatting: Running mypy"
	@poetry run mypy
	@echo "🚀 Checking for obsolete dependencies: Running deptry"
	@poetry run deptry .

test: ## Test the code with pytest
	@echo "🚀 Testing code: Running pytest"
	@poetry run pytest --cov --cov-config=pyproject.toml --cov-report=xml

clean-build: ## clean build artifacts
	@rm -rf dist

build: clean-build ## Build wheel file using poetry
	@echo "🚀 Creating wheel file"
	@poetry build
	@echo "🚀 Checking artifacts created in the previous step"
	@poetry run twine check dist/*

publish:  ## Publish package to Azure Artifact
	@echo "🚀 Publishing packge to Azure Artifacts "
	@poetry run twine upload -r kpatryk dist/*

build-and-publish: build publish ## Build and publish.

docs-test: ## Test if documentation can be built without warnings or errors
	@poetry run mkdocs build -s

docs: ## Build and serve the documentation
	@poetry run mkdocs serve

.PHONY: docs

.PHONY: help

help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-20s\033[0m %s\n", $$1, $$2}'

.DEFAULT_GOAL := help
