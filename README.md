# web-app
# first wrote the app.py file where will be the source code of the application
nano app.py 
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World! This is my basic Flask web application.'

if __name__ == '__main__':
    app.run(debug=True
# on the server the app will run on the public ip and :5000  or  flask run on the =0.0.0.0

# then the test_app.py file for the test 
    nano test_app.py
    import unittest
from app import app

class TestFlaskApp(unittest.TestCase):

    def setUp(self):
        app.testing = True
        self.app = app.test_client()

    def test_index_route(self):
        """Test the index route."""
        response = self.app.get('/')
        self.assertEqual(response.status_code, 200)
        self.assertEqual(response.data.decode('utf-8'), 'Hello, World! This is my basic Flask web application.')

    def test_invalid_route(self):
        """Test an invalid route."""
        response = self.app.get('/invalid')
        self.assertEqual(response.status_code, 404)

if __name__ == '__main__':
    unittest.main()

# go to heruku app log in and generate the api and create a new app and fill the details the in the .yml file 

# now the ci/cd workflow .yml file 
name: CI/CD

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.9

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run tests
        run: pytest

      - name: Deploy to Heroku
        if: success()
        uses: akhileshns/heroku-deploy@v3.12.12
        with:
          heroku_api_key: ${{ secrets.HRKU-663d4aa7-1945-4155-ab9a-2c30e4340ef2 }}
          heroku_app_name: "myapp"
          heroku_email: "pathanzaher65@gmail.com"
          

    
