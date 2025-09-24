
# Detailed instructions on setting up Python and installing `uv` on ONS machines

## Setting up Python on ONS PCs
Make sure you have git and Python installed on your computer (using Service Now) and set up python and pip using these instructions [ASAP wiki](https://gitlab-app-l-01/ASAP/coding-getting-started-guide/-/wikis/python).

It is useful to follow the ASAP instructions above to create a `.bat` file that will enable you to access that version of Python using with a shortcut, such as `python3_11`. You can then use that to replace
`<path_to_python>` below.

## 2. Installing uv for the virtual environment and package management
This section can be skipped if you have performed it for a different project.

In order to install uv on your Windows machine so it is not restricted to a particular 
environment, use pipx. You may first need to install pipx:
```
<path_to_python> -m pip install pipx
```
To ensure your environment PATH is updated, run the following:
```
pipx ensurepath
```
After this you will need to restart your terminal.
You are now ready to install uv:
```
pipx install uv
```
and again update your path:
```
pipx ensurepath
```
Again, restart your terminal, and now `uv` will be available globally.

There is one more step to ensure `uv` will use the ONS Aritfactory and the ONSApps version of Python. Create a toml file in this location:

```
%APPDATA%\uv\uv.toml
```
`%APPDATA%` can be accessed by pasting in the navigation bar in Windows Explorer or by navigating to `C:\\Users<windows_username>\AppData\Roaming`

Paste in the following, replacing `<username>` and `<encr_password>` with your windows username and encripted password respectively.

```
cache-dir = "D:/uv/cache"

allow-insecure-host = ["onsart-01"]
python-preference = "only-system"
python-downloads = "never"

[[index]]
url = "https://<username>:<encr_password>@onsart-01/artifactory/api/pypi/yr-python/simple"
default = true
```

(see [`uv`'s documentation](https://docs.astral.sh/uv/getting-started/installation/#pypi) for alternative installation methods)

## 3. Setting up a virtual environment using `uv` and the ONSApps Python version

### 3a. Method 1: create a venv explicitly using your version of python

To create a virtual environment, simply open a terminal and type
```
python3_11 -m venv .venv
```

To activate the environment, run this:
```
.venv\Scripts\activate
```

**Advantages:**

* Guarantees the venv uses the exact Python interpreter you specify, regardless of PATH order.
* Most portable and standard method—works everywhere Python is installed.
* No dependency on uv for venv creation; users only need Python.
* Ensures compatibility in environments with multiple Python versions or strict IT controls.

**Disadvantages:**

* You cannot use commands like `uv tool run ...` unless you explicitly install tools with 
`uv tool install ...` which then doesn't make it so reproduceable.
* Slightly more manual, as you must specify the full path to Python.

### 3b. Method 2: use uv to create the venv
In this method, you need to only have one version of Python installed, or make sure
the version of python you are using is the first in your PATH. 

It will also need to be the first item in your PATH every time you restart the terminal 
and activate the environment. In this cas you can simply setup your venv with

```
uv venv
```

**Advantages:**

* Convenient: creates a venv using the first Python found in your PATH.
* Integrates with uv’s tool management features (e.g., uv tool run ... works out of the box if tools are installed with uv tool install ...).
* Good for users who have a single, well-configured Python in their PATH.

**Disadvantages:**

* Does not let you directly specify a Python path; relies on PATH order.
* If multiple Pythons are installed, may use the wrong one unless you adjust PATH.
* Less portable in locked-down or multi-Python environments.
* If your required Python is not first in PATH, you must manually update PATH before running `uv venv` or on restarting the terminal
