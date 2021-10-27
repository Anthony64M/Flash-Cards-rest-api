# Flash-Cards REST API Documentation


This is a REST API for flash cards. It is a simple, fast and easy way to create, edit and delete flash cards. It is also a way to share your flash cards with other people.

The entire application is built on django REST framework. It is a powerful framework that allows you to create RESTful APIs in a very simple way.

It also contains a simple user authentication system. It is very easy to use and very secure.

## Setup Requirements

    - Git
    - Python 3.8
    - Django 3.2
    - Django REST framework 3.12
    - PostgreSQL
    - Postman
    - Cloudinary
         - CLOUD_NAME
         - API_KEY
         - API_SECRET

    - Heroku cli (if you want to deploy to Heroku)

## Setup Installation

    - Clone the repository
    - Run the following commands in the terminal:
        - cd <path_to_project> (if you cloned the repository)
        - virtualenv env
        - source env/bin/activate
        - pip install -r requirements.txt
        - cp .env.example .env
        - python manage.py makemigrations
        - python manage.py migrate
        - python manage.py runserver
    - Open Postman to test the API endpoints or use the following link:
        - http://localhost:8000/api/<the_endpoint>

# REST API

The REST API to the flashcards app is described below.

## Get list of Subjects

### Request

`GET /api/subjects/`

    curl -i -H 'Accept: application/json' http://127.0.0.1:8000/api/subjects/

### Response

    HTTP 200 OK
    Allow: GET, POST, HEAD, OPTIONS
    Content-Type: application/json
    Vary: Accept

    [
        {
        "id": 4,
        "name": "science",
        "created_at": "2021-10-26T15:20:29.583538+03:00",
        "updated_at": "2021-10-26T15:20:29.583559+03:00"
       },
    ]

## Create a new Subject

### Request

`POST /api/subjects/`

    curl -i -H 'Accept: application/json' -d 'name=chemistry' http://127.0.0.1:8000/api/subjects/

### Response

    HTTP/1.1 201 Created
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 201 Created
    Connection: close
    Content-Type: application/json
    Location: /thing/1
    Content-Length: 36

    {
        "id": 7,
        "name": "chemistry",
        "created_at": "2021-10-26T20:22:05.483774+03:00",
        "updated_at": "2021-10-26T20:22:05.483800+03:00"
    }

## Get a specific Subject

### Request

`GET /api/subjects/id/`

    curl -i -H 'Accept: application/json' http://127.0.0.1:8000/api/subjects/4/

### Response

    HTTP/1.1 200 OK
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 36

    {
        "id": 4,
        "name": "science",
        "created_at": "2021-10-26T15:20:29.583538+03:00",
        "updated_at": "2021-10-26T15:20:29.583559+03:00"
    }

## Get a non-existent Thing

### Request

`GET /api/subjects/id/`

    curl -i -H 'Accept: application/json' http://localhost:7000/thing/9999

### Response

    HTTP/1.1 404 Not Found
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 404 Not Found
    Connection: close
    Content-Type: application/json
    Content-Length: 35

    {
        "detail": "Not found."
    }

## Create new Note

### Request

`POST /api/notes/`

    curl -i -H 'Accept: application/json' -d 'user=1&title=study computer&description=&subject=3' http://localhost:7000/api/notes/

### Response

    HTTP/1.1 201 Created
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 201 Created
    Connection: close
    Content-Type: application/json
    Location: /thing/2
    Content-Length: 35

    [
        {
            "id": 1,
            "user": 1,
            "title": "study computer",
            "description": "Most computers....",
            "subject": 3,
            "created_at": "2021-10-25T22:33:13.053112+03:00",
            "updated_at": "2021-10-26T15:37:37.802552+03:00"
        }
    ]

## Get list of Notes

### Request

`GET /api/notes/`

    curl -i -H 'Accept: application/json' http://127.0.0.1:8000/api/notes/

### Response

    HTTP/1.1 200 OK
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 74

    [
        {
            "id": 1,
            "user": 1,
            "title": "study computer",
            "description": "Most computers....",
            "subject": 3,
            "created_at": "2021-10-25T22:33:13.053112+03:00",
            "updated_at": "2021-10-26T15:37:37.802552+03:00"
        }
    ]

## Get a specific Note

`GET /api/notes/id/`

    curl -i -H 'Accept: application/json' http://127.0.0.1:8000/api/notes/1/

### Response

    HTTP/1.1 200 OK
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 74

    [
        {
            "id": 1,
            "user": 1,
            "title": "study computer",
            "description": "Most computers....",
            "subject": 3,
            "created_at": "2021-10-25T22:33:13.053112+03:00",
            "updated_at": "2021-10-26T15:37:37.802552+03:00"
        }
    ]

## Update a Note

`PUT /api/notes/id/`

    curl -i -H 'Accept: application/json' -d 'user=1&title=study computer&description=&subject=3' http://127.0.0.1:8000/api/notes/1/

### Response

    HTTP/1.1 200 OK
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 35

    [
        {
            "id": 1,
            "user": 1,
            "title": "study computer",
            "description": "Most computers....",
            "subject": 3,
            "created_at": "2021-10-25T22:33:13.053112+03:00",
            "updated_at": "2021-10-26T15:37:37.802552+03:00"
        }
    ]

## Delete a Note

`DELETE /api/notes/id/`

    curl -i -H 'Accept: application/json' http://127.0.0.1:8000/api/notes/1/

### Response

    HTTP/1.1 204 No Content
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 204 No Content
    Connection: close
    Content-Length: 0

## Get Profiles

`GET /api/profiles/`

    curl -i -H 'Accept: application/json' http://127.0.0.1:8000/api/profiles/

### Response

        HTTP/1.1 200 OK
        Date: Thu, 26 Oct 2021 12:36:30 GMT
        Status: 200 OK
        Connection: close
        Content-Type: application/json
        Content-Length: 74

        [
            {
                "user": 1,
                "bio": "",
                "profile_pic": "image/upload/picha link",
                "contact": "",
                "location": "",
                "notes": [],
                "created_at": "2021-10-26T15:44:22.778462+03:00",
                "updated_at": "2021-10-26T15:44:22.778481+03:00"
            }
        ]

## Get a specific Profile

`GET /api/profiles/id/`

    curl -i -H 'Accept: application/json' http://127.0.0.1:8000/api/profiles/1/

### Response

        HTTP/1.1 200 OK
        Date: Thu, 26 Oct 2021 12:36:30 GMT
        Status: 200 OK
        Connection: close
        Content-Type: application/json
        Content-Length: 74

        [
            {
                "user": 1,
                "bio": "",
                "profile_pic": "image/upload/picha link",
                "contact": "",
                "location": "",
                "notes": [],
                "created_at": "2021-10-26T15:44:22.778462+03:00",
                "updated_at": "2021-10-26T15:44:22.778481+03:00"
            }
        ]

## Update a Profile

`PUT /api/profiles/id/`

    curl -i -H 'Accept: application/json' -d 'user=1&bio=&profile_pic=&contact=&location=' http://127.0.0.1:8000/api/profiles/1/

### Response

    HTTP/1.1 200 OK
    Date: Thu, 26 Oct 2021 12:36:30 GMT
    Status: 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 74

    [
        {
            "user": 1,
            "bio": "",
            "profile_pic": "image/upload/house.png",
            "contact": "",
            "location": "",
            "notes": [],
            "created_at": "2021-10-26T15:44:22.778462+03:00",
            "updated_at": "2021-10-26T15:44:22.778481+03:00"
        }
    ]

## User List

### Request

`GET /api/users/`

        curl -i -H 'Accept: application/json' http://127.0.0.1:8000/api/users/

### Response

        HTTP/1.1 200 OK
        Date: Thu, 26 Oct 2021 12:36:30 GMT
        Status: 200 OK
        Connection: close
        Content-Type: application/json
        Content-Length: 74

        [
            {
                "id": 1,
                "username": "admin",
                "first_name": "",
                "last_name": "",
                "email": "
            }
        ]

## Create New User

`POST api/users/create/`

    curl -i -H 'Accept: application/json' -d '  http://127.0.0.1:8000/api/users/create/

### Response

        HTTP/1.1 201 Created
        Date: Thu, 26 Oct 2021 12:36:30 GMT
        Status: 201 Created
        Connection: close
        Content-Type: application/json
        Content-Length: 74

        [
            {
                "id": 1,
                "username": "admin",
                "first_name": "",
                "last_name": "",
                "email": "
            }
        ]

## User Login

`POST api/auth/login/`

    curl -i -H 'Accept: application/json' -d 'username=admin&password=admin' http://127.0.0.1:8000/api/auth/login/

### Response

            HTTP/1.1 200 OK
            Date: Thu, 26 Oct 2021 12:36:30 GMT
            Status: 200 OK
            Connection: close
            Content-Type: application/json
            Content-Length: 74

            [
                {
                    "id": 1,
                    "username": "admin",
                    "first_name": "",
                    "last_name": "",
                    "email": "
                }
            ]

## Logout User

`POST api/auth/logout/`

    curl -i -H 'Accept: application/json' -d 'username=admin&password=admin' http://127.0.0.1:8000/api/auth/logout/

### Response

            HTTP/1.1 200 OK
            Date: Thu, 26 Oct 2021 12:36:30 GMT
            Status: 200 OK
            Connection: close
            Content-Type: application/json
            Content-Length: 74

## Known Bugs

So far so good there are no bugs related to this project 😎

## Support and contact details 🙂

To make a contribution to the code used or any suggestions you can click on the contact link and email me your suggestions.

- Email: jymal6anthony4@gmail.com
- Phone: +254721229683

## License

* [![License](https://img.shields.io/packagist/l/loopline-systems/closeio-api-wrapper.svg)](https://github.com/Anthony64M/Picture-Globe/blob/master/LICENSE)  
* Copyright (c) 2021 **Anthony64M **