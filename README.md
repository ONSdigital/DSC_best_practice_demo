# TODO

Summary of repository scope / use case

## Installation

TODO

```bash
todo
```

## Usage

```bash
todo
```

## Contributing

#### Clone the repo

```bash
git clone "git@github.com:owner/repo_name.git"
```
#### Make a virtual environment 

###### Only for Debian Cloud Workstation:
```bash
sudo apt update ; sudo apt install python3-venv
```

###### For everyone:

```bash
python3 -m venv .todo_venv
source .todo_venv/bin/activate
pip install poetry
```

#### Configure your virtual environment with poetry
```bash
poetry lock
poetry install
``` 
#### Set up pre-commit hooks
```bash
make setup-git-hooks
```


## License

[MIT](https://choosealicense.com/licenses/mit/)