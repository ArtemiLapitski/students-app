## Web framework: Flask restful api

It is an application that inserts/selects/updates/deletes data in the database using sqlalchemy and flask rest framework.


## Installation

Clone a project:
```
git clone https://github.com/ArtemiLapitski/students-app.git
```

Open project directory:
```
cd students-app
```

Create a virtualenv or skip this point.
Activate virtualenv.

Install the requirements:
```
pip install -r requirements.txt
```

Create the file .env.  Use .env.example file as example.

Make sure you have docker installed. Run docker daemon.

Build docker image:
```
docker build -t students-app .
```

Run docker image:
```
docker run --env-file .env students-app
```

Run server:

On Win:
```
set FLASK_APP=main.py
```
On Mac:
```
export FLASK_APP=main.py
```
Then:
```
flask run
```

Urls: http://127.0.0.1:5000


## Project description:

The database will be filled with test data upon setting up the app (described in the Installation section above). 
200 students, 10 groups and 10 courses are randomly generated. 
Students are then randomly assigned to groups and courses.
10 to 30 students are assigned to each group.
Some groups may be without students or students without groups.
1-3 courses are assigned to each student.


## Usage:

Examples of the allowed API requests are presented below.

- Get groups which contain less than or equal to amount of students.

GET: http://127.0.0.1:5000/groups?student_count_lte=15

Example response:
```
[
    "SK-11",
    "BW-86",
    "SI-60",
    "YU-31"
]
```

- Find all students related to the course with the given name.

GET: http://127.0.0.1:5000/students?course=Art

Example response:
```
[
    "Essence Lowe",
    "Shyann Fletcher",
    "Brenna Armstrong",
    "Jackson Rush",
    "Raphael Best"
]
```

- Add new student.

PUT: http://127.0.0.1:5000/students

Body of the request:
```
{"first_name": "George", "last_name": "Washington", "courses": ["Art", "Science", "Physics"]}
```

Example response (group will be null if not specified in request):
```
{
    "student_id": 201,
    "first_name": "George",
    "last_name": "Washington",
    "courses": [
        "Art",
        "Science",
        "Physics"
    ],
    "group": null
}
```

- Delete student by STUDENT_ID.

DELETE: http://127.0.0.1:5000/students/1

Example response:
```
{
    "mssg": "Student under id '1' has been deleted"
}
```

- Add student (STUDENT_ID=2) to the course (COURSE_ID=3).

PUT: http://127.0.0.1:5000/students/2/courses/3

Example response:
```
{
    "student_id": 2,
    "first_name": "Colten",
    "last_name": "Alvarez",
    "courses": [
        "Science",
        "Art",
        "English"
    ],
    "group": null
}
```

- Delete student (STUDENT_ID=2) from course (COURSE_ID=3).

DELETE: http://127.0.0.1:5000/students/2/courses/3

Example response:
```
{
    "mssg": "Course under id '3' has been deleted"
}
```
