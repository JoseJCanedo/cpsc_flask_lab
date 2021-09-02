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
