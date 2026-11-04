# Online Course Platform with Exams (Django)

A Django web app for online courses, where learners register, enroll in courses, read lessons, and **take multiple-choice exams** that are graded automatically.

Built as the final project of the IBM *Django Application Development with SQL and Databases* course. I added the whole assessment feature (models, views, templates and admin) to a starter course app.

## Features

- **User accounts.** Registration, login and logout using Django's auth system.
- **Courses and enrollment.** Browse courses and enroll in them. Enrolled learners see the course lessons.
- **Exams.** Each course has questions with multiple choices, and a question can have more than one correct answer.
- **Automatic grading.** Submitted answers are saved as a `Submission`. The results page shows the score, highlights correct and incorrect choices, and shows pass or fail.
- **Admin panel.** Instructors manage courses, lessons, questions and choices. Choices are edited inline with their question.

## Data model

```
Instructor ─┐
            ├─< Course >─── Lesson
Learner ────┘     │
                  ├──< Enrollment >── User
                  └──< Question ──< Choice
                                       │
                  Submission >─────────┘  (many-to-many: selected choices)
```

Models: `Instructor`, `Learner`, `Course`, `Lesson`, `Enrollment`, `Question`, `Choice`, `Submission`

## Key views

| View | What it does |
| --- | --- |
| `enroll` | Enrolls the logged-in user in a course |
| `submit` | Collects the selected choices from the exam form and creates a `Submission` |
| `extract_answers` | Reads the selected choice IDs from the POST data |
| `show_exam_result` | Works out the total score against each question's correct answers and renders the results |

## Running it

```bash
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser      # to add courses and exams in /admin
python manage.py runserver            # http://localhost:8000/onlinecourse
```

## Tech stack

Python · Django 4.2 · SQLite · Bootstrap · Gunicorn (deployment-ready with `Procfile` and `manifest.yml`)
