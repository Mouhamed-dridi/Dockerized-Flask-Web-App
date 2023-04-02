# Dockerized-Flask-Web-App
Flask-Docker-Web-Template is a simple template for creating and deploying Flask web apps in Docker. It includes a basic Flask app structure and Dockerfiles to get developers up and running quickly.


## Install Docker 
first step install docker in you linux machine can you flow this guid check url : https://phoenixnap.com/kb/install-docker-on-ubuntu-20-04

## Create Flaskapp
Create a new directory for your project and navigate to it in your terminal.

Create a new Python file called app.py 

```
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')


```
# Create requirements.txt

is a text file that lists the Python packages required by your Flask application, and is typically used when building a Docker image for your application to ensure that the required packages are installed in the container.
```
click==8.0.3
colorama==0.4.4
Flask==2.0.2
itsdangerous==2.0.1
Jinja2==3.0.3
MarkupSafe==2.0.1
Werkzeug==2.0.2
gunicorn==20.1.0
```


## Create Dockerfile

In this Dockerfile, we're using the official Python 3.9 image as the base image. We're setting the working directory to /app, copying the requirements file into the container, and installing the dependencies with pip. Then, we're copying the entire current directory into the container at /app, exposing port 5000 for the Flask app to run on, setting the FLASK_APP environment variable, and running the flask run command to start the Flask app.

```
# Use an official Python runtime as a parent image
FROM python:3.9-alpine

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN mkdir templates
COPY index.html templates/

EXPOSE 5000

CMD [ "python", "app.py" ]
# Run the command to start the Flask app
CMD ["flask", "run", "--host=0.0.0.0"]

```


## Run Your Project
```
docker build -t my_flask_app .
docker run -p 5000:5000 my_flask_app
```
