# Overview

This repository acts as a template, for quickly spinning up new Python-based projects with pre-configured security features, linting and package-management.

To create a new repository from this template, click the green 'Use this template' button at the top right of this page.

## Installation

* Assuming you have created a new repository from this template, clone that repository locally with 
```bash
git clone <your repo's clone link>
```

* Next, change directory to your newly cloned repository with 
```bash
cd <your repo's name>
```

>**Windows users:**
>NOTE: if you are working on Windows, there are a few extra steps.
> 
>First, set up a virtual environment and activate it using the following commands 
>in the terminal:
>```
><path-to-python> -m venv .venv
>```
>```
>.venv\Scripts\activate
>```


* Install `uv` for package management and orchestration of package build processes with 
```bash
pip install uv
```
(see [`uv`'s documentation](https://docs.astral.sh/uv/getting-started/installation/#pypi) for alternative installation methods)

* Install the project and it's dependencies in a `uv`-managed virtual environment with
```bash
# build the lockfile to persist exact package versions
uv lock
# install the packages specified in the lockfile
uv sync
```

## Packaging

To create an installable package for the current project, you can run
```bash
uv build
```
which will create a `dist/` directory containing `pip install`-able package files in both `.tar.gz` and `.whl` formats.

## Contributing

#### For people who are developing your project, not just using it

#### Set up pre-commit hooks
This template comes with `pre-commit` hooks configured for best practices, linting and security.
On each `git commit` and `git push`, it runs validation checks and security checks using `bandit` and `gitleaks`, which must pass for the commit / push to be carried out.

`bandit` and `gitleaks` are described in more detail in the Security section, below.

```bash
make setup-git-hooks
```

#### Security

Forking this template under the `ONSdigital` GitHub group will provide access to GitHub Enterprise level security enhancements in GitHub, including ongoing dependancy scanning and reporting via Dependabot, and GitGuardian checks when Pull Requests are opened.

Additionally, we include `bandit` and `gitleaks` checks in the pre-commit hooks that we provide, to prevent API key / secret leaks making it as far as a (potentially public) remote GitHub repository.

* `bandit`: a Python security tool, which scans code to identify bad / dangerous practices. See [the documentation](https://bandit.readthedocs.io/en/latest/) for more detail.

* `gitleaks`: a pattern-based security tool, used to identify strings that match the form of API keys / other secrets that should not be made public. `gitleaks` is not as robust as GitGuardian, but has the advantage of being able to be used locally, and as a free and open-source package it can be used for repositories not under a GitHub Enterprise licence. See [the documentation](https://github.com/gitleaks/gitleaks) for more detail.

## License

[MIT](https://choosealicense.com/licenses/mit/)