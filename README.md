# Flask Starter
An example of a simple micro-service using Pythons's Flask framework.

I also provide a set of instructions to completely set up a Flask project and
deploy to AWS Lambda using Zappa.

## Setup the Python environment
Open up terminal (I only provide Mac instructions) and with Homebrew installed
run the following commands;
    # install python
    $ brew update
    $ brew install python3
## Setup the project and create the web application
Now setup a new project and create a trivial web application using Flask.
First, we have to execute some shell commands to create our new project.
    # create an empty directory for our project
    $ mkdir flaskstarter
    $ cd flaskstarter

    # Init the Pipfile and a virtual environment for the project.
    $ pipenv --three

    # activate the virtual environment
    $ pipenv shell

    # install Zappa and Flask along with the AWS command line tools
    $ pipenv install zappa flask
    $ pipenv install --dev awscli

    # optionally install some handy development tools inside the virtual environment
    $ pipenv install --dev flake8 autopep8 ipython

Next we create a file named app.py inside the directory flaskstarter. A real flask application will have additional files but to validate this process we could have the following code (below) which simply returns "hello world" message at the root url.

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return "Hello, world!", 200

# We only need this for local development.
if __name__ == '__main__':
    app.run()
```

Finally, we can fire up our local debug server and test our simple web application.
    # export and run application
    $ export FLASK_APP=hello_world.py
    $ flask run

You can reach it by opening the url http://127.0.0.1:5000/ in your browser.

## Configure your AWS credentials and default region
Before we deploy our web application, we have to make sure we have a valid AWS account and our AWS credentials and default region is properly configured on the development machine.

All this can be done with the AWS Command Line Tools.
    # configure your AWS keys (this should be done outside the pipenv)
    $ aws configure

This prompts us to fill in the access key id, the secret access key and the default region.

Now our AWS account is setup on our development machine and we can start to configure Zappa and deploy our application to AWS Lambda.

## Configure Zappa and deploy
So far we have a setup our project, added a simple web application and configured our AWS account. Now, we can prepare our project to be managed and deployed by Zappa. In order to do this, we just have to run the following command inside the project directory.
    # initialise zappa config
    $ zappa init

This creates a file named zappa_settings.json inside your project directory.
Next we deploy to AWS
    # deploy
    $ zappa deploy
