# Installation setup

`brew install mkdocs`

`git clone git@github.com:uwrit/infra-docs.git`

`cd infra-docs`

`mkdocs serve`

# alternative Native Python setup
check Python is greater than 3
```
$ python -V
Python 3.8.7
```
then setup a virtual environment (called venv here) and install mkdocs...
```
  $  python -m venv venv
  $  source ./venv/bin/activate
  $  pip install --upgrade pip
  $  pip install mkdocs
  $  mkdocs serve
```

# Updating changes to onboard.rit.uw.edu

1. Change files as needed on any branch
2. Merge changes to master
3. Run command `mkdocs gh-deploy`

onboard.rit.uw.edu should update automatically

Note: keep CNAME file in docs/CNAME

Mkdocs GitHub pages deployment reference: https://www.mkdocs.org/user-guide/deploying-your-docs/
