# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Endpoints documentation

Endpoints:
GET '/categories'
GET '/questions'
POST '/questions'
DELETE '/questions/<int:id>'
POST '/questions/search'
GET '/categories/<int:id>/questions'
POST '/quizzes'

A description of each endpoint follows.

GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, categories, that contains a object of id: category_string key:value pairs. 
{'1' : "Science",
'2' : "Art",
'3' : "Geography",
'4' : "History",
'5' : "Entertainment",
'6' : "Sports"}

GET '/questions'
- Fetches a dictionary of paginated questions (10 per page) in which the keys are the ids of the questions, answer, category and difficulty.
- Request Arguments: None
- Returns an object with the following keys:
        - 'questions': a paginated object whose keys correspond to each question (described below):
        - 'id' - question id
        - 'question' - Question text.
        - 'answer' - Question answer text.
        - 'category': Question category id.
        - 'difficulty': A number from 1 to 5, with 1 being the least difficult and 5 being the most difficult.
    - 'total_questions' - The number of total questions.
    - 'current_category' - 'None'
    - 'categories': A dictionary of categories, just the same as that returned by the GET '/categories' endpoint.

POST '/questions'
- Takes a dictionary for the creation of a new question.
- Request Arguments: - 'question' - Question text.
                     - 'answer' - Question answer text.
                     - 'category': Question category id.
                     - 'difficulty': A number from 1 to 5, with 1 being the least difficult and 5 being the most difficult.
- Returns an object with the following keys:
    - 'success' - True
    - 'created' - The created question id
    - 'questions' - a paginated object whose keys correspond to each question (described in the GET '/questions' endpoint)
    - 'total_questions' - The number of total questions.

DELETE '/questions/<int:id>'
- Request Arguments: The id of the question to be deleted.
- Deletes the given question and returns a dictionary with the following keys:
    - 'success' - True
    - 'deleted' - The deleted question id
    - 'questions' - a paginated object whose keys correspond to each question (described in the GET '/questions' endpoint)
    - 'total_questions' - The number of total questions.

POST '/questions/search'
- Fetches a dictionary of questions which correspond to the search term given.
- Request Arguments: 'searchTerm'
- Returns: An object with the follwing keys:
    - 'success' - True
    - 'questions' - a paginated object whose keys correspond to each question (described in the GET '/questions' endpoint)
    - 'total_questions' - The number of total questions.
    - 'current_category' - 'None'

GET '/categories/<int:id>/questions'
- Fetches a dictionary of questions which correspond to the category specified.
- Request Arguments: the id of the cetegory.
- Returns: An object with the follwing keys:
    - 'success' - True
    - 'questions' - a paginated object whose keys correspond to each question (described in the GET '/questions' endpoint)
    - 'total_questions' - The number of total questions.
    - 'current_category' - 'None'

POST '/quizzes'
- Allows playing of the game. Fetches a dictionary of a new question and the previous questions.
- Request Arguments:
    - 'previous_questions' - a list of the previous question ids used in the current game. This should be an empty list when a new game is started.
    - 'quiz_category' - a dictionary with the following keys:
        - 'type' - the text description of the category (e.g. 'Science')
        - 'id' - the category id
- Returns: An object with the follwing keys:
    - 'success' - True
    - 'question' - A dictionary of the next questions details. Keys:
        - 'id' - question id
        - 'question' - Question text.
        - 'answer' - Question answer text.
        - 'category': Question category id.
        - 'difficulty': A number from 1 to 5, with 1 being the least difficult and 5 being the most difficult.
    - 'previous_questions': - a list of the previous question ids used in the current game.

## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```