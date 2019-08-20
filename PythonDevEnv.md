# Setting Python development environments for OSX

These instructions are based on:
* [Setting up Python development environment on Mac OS X](https://www.techsfo.com/blog/2016/06/setup-python-mac-os-x/)
* [pyenv plugin to manage virtualenv](https://github.com/pyenv/pyenv-virtualenv)
* [Working with Matplotlib on OSX](https://matplotlib.org/faq/osx_framework.html)

## Prerequisites

Assuming that you have already installed [Homebrew](https://brew.sh)

## pyenv

Install Python Version Management tool [pyenv](https://github.com/pyenv/pyenv)
```bash
brew install pyenv
brew install pyenv-virtualenv         # plugin to work with virtual environments
```

To load pyenv automatically when shell starts add lines as follows to ~/.bash_profile
```bash
# Python from pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

## Python

Install Python Framework install in order to be able to work with Matplotlib and other libs requiring GUI.

I prefer to install both Python 2 and Python 3 versions.

```bash
# currently released versions are 2.7.15, 3.6.5
PYTHON_CONFIGURE_OPTS="--enable-framework" pyenv install 2.7.15
PYTHON_CONFIGURE_OPTS="--enable-framework" pyenv install 3.6.5  
```

## Project specific virtual environments

* Create: `pyenv virtualenv 2.7.10 my-virtual-env-2.7.10`
* List: `pyenv virtualenvs`
* Activate manually: `pyenv activate my-virtual-env-2.7.10`
* Activate automatically on entering folder:
  execute in a folder `pyenv local my-virtual-env-2.7.10` to associate the
  virtual environment with the folder and its subfolders.
* Deactivate: `pyenv deactivate`
* Delete: `pyenv uninstall my-virtual-env-2.7.10`

Here `2.7.10` is a Python version, `my-virtual-env-2.7.10` is the name of a virtual environment.


##See also
* https://github.com/pyenv/pyenv
* https://github.com/pyenv/pyenv-virtualenv
* https://github.com/pyenv/pyenv-virtualenvwrapper


##Troubleshooting

###Error zipimport.ZipImportError: can't decompress data; zlib not available
####Option 1
Update command line tools (on OSX)
```bash
xcode-select --install
```
####Option that worked for me (credits to dukeyu1991)
```bash
CFLAGS="-I$(xcrun --show-sdk-path)/usr/include" pyenv install 2.7.6
```

