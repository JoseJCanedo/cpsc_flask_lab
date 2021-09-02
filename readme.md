# Flask Tutorial Part 1:

Flask is a micro framework for building websites using html templates in Python. For this app we will be using GitHub and GitPod for this lab. By the end of part 1 we will have a Python Flask website that returns a template with bootstrap and some external CSS we add. 

We are starting with Python Flask because it is a simple framework and Python is one of the first coding languages you probably learned. Its quick and easy to start a website using this.

Lets start off by creating a repo in GitHub called **Flask_lab** and opening it in GitPod. Please be sure to make sure its public and that it is initialized with a readme.

Now that we have this open in GitPod you can check to see the version of python installed with the following command in the terminal.

```
python --version
```
You should get a response back like: **Python 3.8.11**

Now lets create our Python file and call it **app.py**

We are going to start with the traditional Hello World! like with all other programming languages. 

Within **app.py** add the following code:
```python
from flask import Flask           # import flask framework
app = Flask(__name__)             # create an app instance

@app.route("/")                   # use the home url
def hello():                      # method called hello
    return "Hello World!"         # returns "hello world"
if __name__ == "__main__":        # when running python app.py
    app.run()                     # run the flask app
```
## Running the application

Before we run the application we have to install the Flask framework. We do so by running the following command in the terminal

```
pip install flask
```

Note: *If you fail to install Flask when trying to run the application youll get an error that says **ModuleNotFoundError: No module named 'flask'***

Once that is installed you can run the application with the terminal command:

```
python app.py
```

The application should launch on port 5000 and you will get a popup in GitPod on the lower right hand corner. Select **Open Browser** and youll get a new tab on your browser that will say Hello World.

## Development Mode

Now that you have the application running in port 5000 if you were to go back and make a change you would have to stop the server and restart the application. We dont always want to do that because it could be tedious or time consuming.

For that we use something called debug mode. This will help the application refresh some changes we make without us having to restart the application.

```python
#change app.run() to the following
app.run(debug=True)
```

Turn off the server you are running in the terminal with **ctrl + c**

## Variables
For any websites you interact with you will invariably need to either send information in the URL, known as a path or query parameter, or in the body of the request.

We will be starting with path parameters which are parameters within the URL located before a **?**. Query parameters will be found in a URL after a ? and usually assigned a variable name and variable. 

So after a little back story we will now be passing our names back to the server so it updates the website and instead of saying Hello World it says Hello Jose, or any name you pass it from the URL. 

We will be adding another app.route method. 
```python
@app.route("/<name>")              # route with URL variable /<name>
def hello_name(name):              # call method hello_name
    return "Hello "+ name          # which returns "hello + name  
```

## HTML

Okay now that we have a simple app returning hello world and also hello "insert your name here", lets add a simple HTML file.

Create a new html file and call it **index.html**

```http
<!DOCTYPE html>

```
