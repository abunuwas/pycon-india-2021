# PyCon India 2021, 17-19 September 2021

## Delivering successful API integrations with documentation-driven development

## Author: Jose Haro Peralta

[![image](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jose-haro-peralta/) [![image](	https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/JoseHaroPeralta)

### Full stack consultant

### Co-founder of [microapis.io](https://microapis.io)

### Author of [Microservice APIs in Python](https://www.manning.com/books/microservice-apis-in-python)

- 35% discount code: **ctwpyconin21**
- Download two chapters of the book for free from this [link](https://www.microapis.io/resources/microservice-apis-in-python).


## How to work with this repo

This repo provides examples for my talk at PyCon India 2021, titled 
"Delivering successful API integrations with documentation-driven development".
The code includes the implementation of a simple TODO REST API in Python, using 
the popular FastAPI framework. The specification for the API is included under 
the [oas.yaml](oas.yaml) file.
To set up the environment required to run the code in this repo, make sure you have:

* Python 3.9 together with pipenv 
* node.js version 12 or higher

To install the dependencies, run the following commands:

```bash
$ pipenv install --dev
$ yarn
```

This will install the Python dependencies required to run and test the app, as well
as the npm dependencies that we use for furhter testing and for server mocking.

To activate the Python environment, run the following command:

```bash
$ pipenv shell
```

Now you can run the TODO API with the following command:

```bash
$ uvicorn todo.server:server
```

To run the Dredd test suite, run the following command:

```bash
$ ./node_modules/.bin/dredd oas.yaml http://127.0.0.1:8000 --server "uvicorn todo.server:app" --hookfiles=./hooks.py --language=python 
```

To run the schemathesis test suite, run the following command, while running the FastAPI server 
with the `uvicorn` command show earlier (`uvicorn todo.server:server`):

```bash
$ schemathesis run oas.yaml --base-url=http://localhost:8000 --stateful=links
```

If you wish to set up your own Travis CI server to test this code, make sure you create a Heroku app with a valid name,
include the name of the app in the deployment file, and run the following command to encrypt your 
deployment key:

```bash
$ travis --encrypt $(heroku auth:token) --add deploy.api_key --pro
```

