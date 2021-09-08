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

Create a new folder called **templates** and within the folder create an html file and call it **index.html**

```xml
<!DOCTYPE html>
<html lang=en dir="ltr">
    <head>
        <meta charset="utf-8">
        <title>CPSC4125 Flask</title>
    </head>
    <body>
        <h1>First Flask HTML page</h1>
        <p>This is a sample</p>
    </body>
</html>
```

Now that we have that HTML file we need to call it so it can be returned to the front end. So we have to go back to our app.py file. We probably want to return it when we go to the home page.

To accomplish this we need to import render_template along with Flask. Change the import to

```python
from flask import Flask, render_template   
```
The second thing we need to do is modify the return on the home page route to return the template instead of "Hello World"

```python
@app.route("/")                
def hello():                    
    return render_template("index.html") 
```

If you refresh your browser running the application on port 5000 you should see the HTML page we added being rendered. If youre still on the page returning your name navigate to the home page.

## Bootstrap

Okay so now in the index.html I want you to navigate to the [Bootstrap website](https://getbootstrap.com/docs/5.1/getting-started/introduction/) and replace the html with the **Starter Template** from the website. Remove the comments in the HTML and replace the title and heading "Hello World" with "Flask App".

## CSS
Since we cant rely on Bootstrap to give us all the styling we need we will be adding a CSS file to this. As with the template Flask will be looking for the CSS in a specific folder.

So lets create a folder named **static** and within that we will create another folder called **css**. Within the folder css lets create our css file and call it **app.css**

```css
h1{
    color: blue;
}
```
With this we now have what we need to import the CSS file into the template. Its not as straight forward as adding in a normal HTML file. We have a little bit of flask specific nuances we need to follow. 

Within index.html we will be adding the link to the stylesheet (css) within the < head > tag and right before the < title > tag
```xml
<link rel="stylesheet" href="{{url_for('static',filename='css/app.css')}}">
```
You should be able to refresh and see the font change to blue.

## Next Steps

On the next part we will be extending this by adding routing to another page, using a template and blocks to prevent duplicate code, and we will setup the page for you to finish this off as your flask+python web app.

Be on the look out for a lecture on APIs as they will be important for us from here on out. 

# Part 2
## Adding Additional Pages

Lets go ahead and create a multi page website instead of a single page. For that we need a new route and we need another page. Lets start on the aboutUs page. Within the templates folder add a file called **about.html**
```xml
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
    <link rel="stylesheet" href="{{url_for('static',filename='css/app.css')}}">
    <title>About</title>
  </head>
  <body>
    <h1>About Me</h1>
    <p>I am writing some information about myself that people can see. </p>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj" crossorigin="anonymous"></script>
  </body>
</html>
```
Within our **app.py** file copy the home route and add "about" to the URL and rename the function to about. DOnt forget to also change the name to about.html instead of index.html. It should look something like this:
```python
@app.route("/about")                
def about():                    
    return render_template("about.html")   
```
If you start the application and change the url to /about you should see your new page come up. 

## Template page
Okay so if youre looking at the about and the home pages you will see some duplicate code. Imagine if we had a nav bar or a footer. Would you want to recreate that multiple times? If you had to update the nav bar do you want to change it in one place or multiple?

To solve this we will be creating a template.html that will act as our template. Fitting, right?

Create a template.html and we will put the following code in it. Please look at the documentation for [url_for()](https://flask.palletsprojects.com/en/2.0.x/api/#flask.url_for). In this class we will also learn how to look for documentation to see how a specific method or API for a language works. Below youll notice we are using a bootstrap nav bar.
```xml
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
    <link rel="stylesheet" href="{{url_for('static',filename='css/app.css')}}">
    <title>Template</title>
  </head>
  <body>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">Navbar</a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
            <div class="navbar-nav">
              <a class="nav-link active" aria-current="page" href="{{ url_for('hello') }}">Home</a>
              <a class="nav-link" href="{{ url_for('about') }}">About</a>
            </div>
          </div>
        </div>
      </nav>
      {% block content %}
      {% endblock %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj" crossorigin="anonymous"></script>
  </body>
</html>
```
The two lines with the curly brackets and blocks will be replaced by the content of home.html and about.html. This will depend on the URL in which the user is browsing.

Now we need to make a small change to about.html and home.html so that they pull in the nav bar by extending template.html and also adding the blocks.

index.html
```xml
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
    <link rel="stylesheet" href="{{url_for('static',filename='css/app.css')}}">
    <title>Hello, world!</title>
  </head>
  <body>
    {% extends "template.html" %}
    {% block content %}
      <h1>Hello, world!</h1>
    {% endblock %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj" crossorigin="anonymous"></script>
  </body>
</html>
```
about.html
```xml
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
    <link rel="stylesheet" href="{{url_for('static',filename='css/app.css')}}">
    <title>about</title>
  </head>
  <body>
    {% extends "template.html" %}
    {% block content %}
        <h1>About Me</h1>
        <p>I am writing some information about myself that people can see. </p>
    {% endblock %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj" crossorigin="anonymous"></script>
  </body>
</html>
```
Youll see we added the same block content and endblock along with the extend for template. 

If you refresh or restart the app you should now see the nav bar showing up at the top and persisting. 

## Passing data from URL to template

Okay so one last task. We are going to learn how to pass a query parameter to the template through the URL.

For that we will use the about and modify the URL so it takes **/about?name=var** with var being your name or some other string. We will also have to handle nulls. 

So lets start by modifying the app.py file.

If you look at the hello_name function we can see how we can accept the path variable, but for this we will be using a query parameter.


We need to be able to access the query parameter. So for that we need to import **request**.
```python
from flask import Flask, render_template, request
```

And then we need to modify the about function to take the query parameter.

```python
@app.route("/about")
def about():
    name = request.arg.get('name')
    return render_template("about.html", aboutName=name) 
```

In this we are taking `name` from the request args and assigning it to a variable named **name**. Last thing we are doing is passing **name** as a variable called **aboutName** to the about template.

Now that we are passing the information we need to modify the about template. Where we had the About Me heading lets change that so that it takes the name from the path. Like with the url_for we need to access the variable using the double curly brace. So we will modify the heading to look like this.

```xml
<h1>About {{ aboutName }}</h1>
```

Start the application and take a look at what we get. If you didnt add the **?name=var** to your url you will notice it says About none. Go ahead and add the query parameter with your name instead of var and you should see it update to About your name. 

We need to be able to handle the none so lets go back to the app.py and add the handling for that. On the line where we assign the query param to name we add the following if statement.

```python
name = request.args.get('name') if request.args.get('name') else "Hello World!" 
```

So in one line we are assigning name from the query parameters to the name variable. If it is null (we just visit /about without the query parameter) assign Hello World. 

Restart the app and play with those changes. 

## Wrap up
So in this lab we learned to use a bit of Flask, routing, rendering html templates, using path parameters in the hello_name function, query parameters in the about template, sending the variable to the template, and extending the nav bar. 

Next Sunday we will be turning in an assignment using most of these concepts for Flask. I am available to answer any questions.
