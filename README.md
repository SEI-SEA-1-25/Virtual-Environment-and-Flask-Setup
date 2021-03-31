# Python Virtual Environments and Flask Set Up

Step by step breakdown of setting up a virtual envrionment for python projects and spinning up a flask app

## Steps to Set up a Virtual Environment with Git

all python projects that use pip packages should be set up to use a virtual environment to ensure version control and package compatibility

#### Basic Virtual Environment Setup

* Create a project directory and cd into it
* run `virtualenv venv` to make a virtual environment
* start the virtual environment before installing needed packages:
  * on mac/linux use `. venv/bin/activate`
  * on windows use `. venv/Scripts/activate`
* make sure your virtual environment is active: `(venv)` can be seen in your terminal
* install the needed pip packages for the project
* once all your packages are installed, freeze the pip list in a requirements.text file
  * use the command `pip freeze > requirements.txt`
  * this needs to be done again if you add more pip packages to update the requirements.txt
  * if you clone a python project from github, you can use `pip install -r requirements.txt` to install the needed packages
* you can use the command `deactivate` to leave the virtual environment
* everytime you want to work on a python project with a virtual environment, you will need to activate it first

#### Virtual Environments with git

the `venv` folder is like `node_modules` with node.js. It needs to be git ignored.

* after you `git init` in your project, `touch .gitignore` and add `venv` and `__pycache__` to it, so they don't get sent up to github.
* if you clone a repo from github with a virtual environment first install the needed packages with `pip install -r requirements.txt` and then run `. venv/bin/activate` (`. venv/Scripts/activate` on windows) to start the virtual environment

## Flask Setup Steps:

The [flask docs](https://flask.palletsprojects.com/en/1.1.x/) are great!

Here are the steps to spin up a flask server:

* First create a virtual environment for your project from the steps outlined in the section above
* install the needed packages for your flask app:
  * `pip install flask` `pip install python-dotenv`
* touch the main entrypoint for your flask app, such as `app.py`
* touch `.flaskenv` and populate it with the needed environmental variables to config flask 
  * .flaskenv doesn't need to be in the .gitignore, it is for flask configuration only. But if you have any API keys or other secrets, you can touch a `.env` file and put them in there.
```sh
# example .flaskenv
# this will enable debug mode in flask
FLASK_ENV=development
# this is main entry point for the flask app
FLASK_APP=app.py
# this is the port to listen on (default is 5000 if you don't specify)
FLASK_RUN_PORT=3000
```
* populate your flask app's entry point file:
```python
# in app.py

# import flask
from flask import Flask

# config app
app = Flask(__name__)

# make route!
@app.route('/')
def hello_world():
  return 'Hello from Flask 👋'
```
* use `flask run` to run your app!
* If you have secret API keys in a `.env` file, you can access them like this:
```python
# import dotenv
from dotenv import load_dotenv
# import the operating system
import os

# this is how you get environmental variables
print(os.environ['MY_BIG_SECRET'])
```
* the corresponding `.env` file would look like this:
```sh
# in .env
MY_BIG_SECRET='pls dont tell anyone my secrets 🙏🏻😳' 
```

*If you add environmental variables while your flask app is running, you need to stop the server with `control + c` and restart it with `flask run` to read them* 
