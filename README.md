# Overview

This repository acts as a template, for quickly spinning up new Python-based projects with pre-configured security features, linting and package-management.

To create a new repository from this template, click the green 'Use this template' button at the top right of this page.

## Installation on an ONS Windows computer

* Assuming you have created a new repository from this template, clone that repository locally with 
```
git clone <link_to_your_repo>
```

* Next, change directory to your newly cloned repository with 
```
cd <name_of_your_repo>
```

>**Windows users:**
>NOTE: if you are working on Windows, there are a few extra steps.
> 
>Follow this link for setting up Python on ONS machines and installing the `uv` package
>and the different options for setting up a virtual environment
>
>[docs/environment_setup.md](docs/environment_setup.md)
>

* To install the packages, activate your virtual environment and then do the following:


First build the lockfile to persist exact package versions:
```
uv lock  
```
Now install the packages specified in the lockfile. If you're not a developer run:
```
uv sync
```

However, if you are a developer and will contribute to the project, you will also need to 
install pre-commits (see below) so *instead* run:
```
uv sync --extra dev
```


## Contributing

#### For people who are developing your project, not just using it

#### Set up pre-commit hooks
This template comes with `pre-commit` hooks configured for best practices, linting and security.
On each `git commit` and `git push`, it runs validation checks and security checks using `bandit`, which must pass for the commit / push to be carried out. Further checks using `gitleaks` are carried out in github on creation of a pull request.

`bandit` and `gitleaks` are described in more detail in the Security section, below.

After completing the setup described above using `uv sync --extra dev`, run
```
pre-commit install
```
This sets up the pre-commit hooks. The first time you actually do a commit, it might take a while, but that will only be a one-off.

#### Security

Forking this template under the `ONSdigital` GitHub group will provide access to GitHub Enterprise level security enhancements in GitHub, including ongoing dependancy scanning and reporting via Dependabot, and GitGuardian checks when Pull Requests are opened.

Additionally, we include `bandit` checks in the pre-commit hooks that we provide, to prevent API key / secret leaks making it as far as a (potentially public) remote GitHub repository.

`bandit` is a Python security tool, which scans code to identify bad / dangerous practices. See [the documentation](https://bandit.readthedocs.io/en/latest/) for more detail.

On creation of a pull request, the github workflow includes checks with `gitleaks`.
`gitleaks` is a pattern-based security tool, used to identify strings that match the form of API keys / other secrets that should not be made public. `gitleaks` is not as robust as GitGuardian, but has the advantage of being able to be used locally, and as a free and open-source package it can be used for repositories not under a GitHub Enterprise licence. See [the documentation](https://github.com/gitleaks/gitleaks) for more detail.

## License

[MIT](https://choosealicense.com/licenses/mit/)