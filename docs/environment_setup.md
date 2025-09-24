
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
