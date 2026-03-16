# Django Modular API Project

## Overview

This project is a modular backend built using **Django** and **Django REST Framework**.
The system manages **Vendors, Products, Courses, Certifications**, and the mappings between them.

The project follows a **modular architecture**, where each entity and mapping is implemented in its own Django app. All APIs are implemented using **APIView only**, without using ViewSets or GenericAPIView.

API documentation is generated using **drf-yasg** with **Swagger UI** and **ReDoc**.

---

# Technologies Used

* Python 3
* Django
* Django REST Framework
* drf-yasg (Swagger API documentation)

---

# Project Structure

```
modular_api_project/
│
├── certification/
├── course/
├── course_certification_mapping/
├── product/
├── product_course_mapping/
├── vendor/
├── vendor_product_mapping/
│
├── modular_api_project/
│   ├── settings.py
│   ├── urls.py
│
├── manage.py
└── README.md
```

---

# Django Apps

## Master Entity Apps

These apps store the main entities.

* vendor
* product
* course
* certification

Each contains:

* models.py
* serializers.py
* views.py
* urls.py
* admin.py

---

## Mapping Apps

These apps store relationships between entities.

* vendor_product_mapping
* product_course_mapping
* course_certification_mapping

Mappings represent:

Vendor → Product
Product → Course
Course → Certification

Each mapping includes:

* parent foreign key
* child foreign key
* primary_mapping flag
* timestamps

---

# Model Fields

## Master Entities

Each master entity includes:

* id
* name
* code (unique)
* description
* is_active
* created_at
* updated_at

---

## Mapping Models

Each mapping model includes:

* parent foreign key
* child foreign key
* primary_mapping
* is_active
* created_at
* updated_at

Duplicate mappings are prevented using unique constraints.

---

# Validation Rules

The following validations are implemented:

* Required field validation
* Unique `code` for master records
* Prevention of duplicate mappings
* Validation of foreign key references
* Only one `primary_mapping=True` allowed per parent entity

Example:

* A vendor cannot be mapped to the same product twice
* A product cannot be mapped to the same course twice
* A course cannot be mapped to the same certification twice

---

# API Design

Each module provides the following APIs:

### List and Create

GET /api/<entity>/
POST /api/<entity>/

### Retrieve, Update, Delete

GET /api/<entity>/<id>/
PUT /api/<entity>/<id>/
PATCH /api/<entity>/<id>/
DELETE /api/<entity>/<id>/

---

# Example API Endpoints

## Vendors

GET /api/vendors/
POST /api/vendors/
GET /api/vendors/<id>/
PUT /api/vendors/<id>/
PATCH /api/vendors/<id>/
DELETE /api/vendors/<id>/

---

## Products

GET /api/products/
POST /api/products/

---

## Courses

GET /api/courses/
POST /api/courses/

---

## Certifications

GET /api/certifications/
POST /api/certifications/

---

## Vendor Product Mapping

GET /api/vendor-product-mappings/
POST /api/vendor-product-mappings/

---

## Product Course Mapping

GET /api/product-course-mappings/
POST /api/product-course-mappings/

---

## Course Certification Mapping

GET /api/course-certification-mappings/
POST /api/course-certification-mappings/

---

# Filtering

Query parameter filtering is supported.

Examples:

```
/api/products/?vendor_id=1
/api/courses/?product_id=2
/api/certifications/?course_id=3
```

This allows retrieving related data efficiently.

---

# API Documentation

API documentation is provided using **drf-yasg**.

### Swagger UI

```
/swagger/
```

### ReDoc

```
/redoc/
```

The documentation includes:

* Request body schema
* Response schema
* Query parameters
* Status codes

---

# Installation and Setup

## 1. Clone the repository

```
git clone <repository-url>
cd modular_api_project
```

---

## 2. Create a virtual environment

```
python -m venv venv
```

Activate it:

Windows

```
venv\Scripts\activate
```

Mac/Linux

```
source venv/bin/activate
```

---

## 3. Install dependencies

```
pip install django
pip install djangorestframework
pip install drf-yasg
```

---

## 4. Run migrations

```
python manage.py makemigrations
python manage.py migrate
```

---

## 5. Create a superuser (optional)

```
python manage.py createsuperuser
```

---

## 6. Run the development server

```
python manage.py runserver
```

Server will run at:

```
http://127.0.0.1:8000/
```

---

# API Testing

You can test the APIs using:

* Swagger UI
* Postman
* Curl
* Insomnia

Swagger automatically generates request and response examples.

---

# Bonus Features

The project also supports:

* Soft delete using `is_active`
* Modular Django app structure
* Clean separation of master and mapping entities
* Timestamp tracking for all records

---

# Author

Django Intern Assignment Submission

Built using Django REST Framework with APIView.

