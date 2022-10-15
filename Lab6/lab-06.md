# Lab 06: Query matching with FastText and Virtex


## Launch a FastText service using the Virtex library in Python
The purpose of this lab is to expose you to a few things:

- The [FastText](https://fasttext.cc/docs/en/python-module.html) library in Python, which is a language modeling and text classification framework

- The idea that NLP systems typically take on the form of microservices, wherein specific functions, such as computing embeddings or computing similar words, are performed in isolation and accessed through HTTP requests (or other protocols such as gRPC).

- A web client such as [Postman](https://www.postman.com/downloads/) or [Advanced Rest Client](https://install.advancedrestclient.com/install), which allows you to make HTTP requests containing data (such as JSON) to the HTTP endpoint hosting your model.

- The [Virtex](https://pypi.org/project/virtex/) library, which provides a convenient way to expose your machine learning computation as a service over HTTP without having to write any networking code (see `query_matcher.py`, `query_matcher.sh`).


## Task I (20 pts)

1. Launch the FastText query matching service by running the following command from the terminal from within the `lab-06/` directory:
    
        $ ./query_matcher.sh

2. Open your REST client (e.g., ARC, Postman)

    - Enter `http://127.0.0.1:8092` into the Request URL bar
    
    - In the Body content type field choose `application/json`

    - Click the body tab and enter `{"data": ["dogs", "bakery", "python", "Python", "florida", "supreme"]}`

    - Explore FastText by changing the words and looking at the matches. Paste of a few of the responses below:

    ``` 
    # Query results go here
    ``` 

### Docker
Virtex will not run on certain machines / environments. If you encounter problems running this code on your machine, you can instead use [Docker](https://www.docker.com/products/docker-desktop/). Once you have docker installed, execute the following commands from within the `lab-06/` directory:

    $ docker build -t fasttext-query-matcher .
    $ docker run --rm --name query-matcher -p 8092:8092 fasttext-query-matcher:latest

And then head over to your rest client (step 2 above) to complete the task. 

### Programmatic interface
As a last resort, you can interact with FastText programmatically from within Python if you are unable to run the query mather on your local machine or in docker, for example:

   ```python
   import compress_fasttext as ft

   model_filepath = "en.model.bin"
   model = ft.models.CompressedFastTextKeyedVectors.load(model_filepath)
   match = model.most_similar("Python")
   print(match)
   ```
