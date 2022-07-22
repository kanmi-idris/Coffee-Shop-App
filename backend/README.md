# Coffee Shop Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Environment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virtual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) and [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) are libraries to handle the lightweight sqlite database. Since we want you to focus on auth, we handle the heavy lift for you in `./src/database/models.py`. We recommend skimming this code first so you know how to interface with the Drink model.

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Running the server

From within the `./src` directory first ensure you are working using your created virtual environment.

Each time you open a new terminal session, run:

```bash
export FLASK_APP=api.py;
```

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## Tasks

### Setup Auth0

1. Create a new Auth0 Account
2. Select a unique tenant domain
3. Create a new, single page web application
4. Create a new API
   - in API Settings:
     - Enable RBAC
     - Enable Add Permissions in the Access Token
5. Create new API permissions:
   - `get:drinks`
   - `get:drinks-detail`
   - `post:drinks`
   - `patch:drinks`
   - `delete:drinks`
6. Create new roles for:
   - Barista
     - can `get:drinks-detail`
     - can `get:drinks`
   - Manager
     - can perform all actions
7. Test your endpoints with [Postman](https://getpostman.com).
   - Register 2 users - assign the Barista role to one and Manager role to the other.
   - Sign into each account and make note of the JWT.
   - Import the postman collection `./starter_code/backend/udacity-fsnd-udaspicelatte.postman_collection.json`
   - Right-clicking the collection folder for barista and manager, navigate to the authorization tab, and including the JWT in the token field (you should have noted these JWTs).
   - Run the collection and correct any errors.
   - Export the collection overwriting the one we've included so that we have your proper JWTs during review!

### Implement The Server

There are `@TODO` comments throughout the `./backend/src`. We recommend tackling the files in order and from top to bottom:

1. `./src/auth/auth.py`
2. `./src/api.py`

barista-JWT->eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IlNhbTRBaDRfdW4xNFZkRy11T3ZrZCJ9.eyJpc3MiOiJodHRwczovL2NvZmVlLXNob3AtYXBwLnVzLmF1dGgwLmNvbS8iLCJzdWIiOiJnb29nbGUtb2F1dGgyfDExMjMxNTM3MTU3NDI0NzQ2NTk4NiIsImF1ZCI6IkNvZmZlZVNob3AiLCJpYXQiOjE2NTg1MzE4NDIsImV4cCI6MTY1ODYxODI0MCwiYXpwIjoiNjBRTXB1NkRCMDY2Wkw1MUtSNTJZQzFDWm11OTJ1d2siLCJzY29wZSI6IiIsInBlcm1pc3Npb25zIjpbImdldDpkcmlua3MiLCJnZXQ6ZHJpbmtzLWRldGFpbCJdfQ.jtFxbpf8G7A7R4O1eH0R7vWUeG0EkW19gos6XjT6g3tl94LlWOtXGWneoUiwUZBq0dl0enGNmhIOwuMDmK34EfdyGTKqrb1THo1hVGSGGxoBoR5mJD8IeWDsgdx17md9g8w8CyLTdO1M6YMt_N5HULJh7KkFg3y1dFsOBCbF0_tR_vx7MG0QFGSXXQYUgvQsXlbaOfK2DQQtsufpvq-3qdaOLi7wnG3IkrrzPVtdfUG8r0TkisDR0aaC1ED_5AzTbfpQ6NO5hd03lgdF5Cr7u2t_usSdtea2IZIKmWgcvPX3bcL86vsvztyoXX9dXM0y7g-PEqeVLCGRmyYVGI07pg

manager-JWT->eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6IlNhbTRBaDRfdW4xNFZkRy11T3ZrZCJ9.eyJpc3MiOiJodHRwczovL2NvZmVlLXNob3AtYXBwLnVzLmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw2MmQ3ZDE4NzA4NDQzMGYxOTI2NTIyNjgiLCJhdWQiOiJDb2ZmZWVTaG9wIiwiaWF0IjoxNjU4NTMyMTg1LCJleHAiOjE2NTg2MTg1ODMsImF6cCI6IjYwUU1wdTZEQjA2NlpMNTFLUjUyWUMxQ1ptdTkydXdrIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6ZHJpbmtzIiwiZ2V0OmRyaW5rcyIsImdldDpkcmlua3MtZGV0YWlsIiwicGF0Y2g6ZHJpbmtzIiwicG9zdDpkcmlua3MiXX0.VMZMkojc9yxNEeDAZBpLS0hwFK8mFOD1r0R_UtpH7lUdRd1zseGXz0XvCefaFnn1X1enrAU_YnYgvmrswHUcMf8flQnFrHfvb88EwibAWF5WHg4KiUdeVYwLf62zPGCClyk9njCAnBryn9LP1OTBtAiAWA0dIoAEHhdoD6_AQskmPDlXBB75NWCTsnOORjT_q976_6VQ7pJTxjbQE18Tg_LhoPhi4V58B-L_xXfwkyaJ_Ey9aQzH5hB2uxPT_MzPstxSzWarAdD6C9tiBXPtcS9kE6pq9FwXV4shEJeCS3aFoukwkQOE8AzQ-wq8JP7si0I1H4HYsxhesRNiBIKi0A
