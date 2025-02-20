# Widi Pustaka

## Overview
Widi Pustaka is a book management API, which provide endpoints to manage books, authors and categories. It support CRUD operations allowing clients to create, read, update and delete resources.

## Table of Contents
- [Installation](#instalation)
- [Configuration](#configuration)
- [API Endpoints](#api-endpoints)
  - [Books](#books)
    - [Index](#booksIndex)
    - [Show](#booksShow)
    - [Create](#bookCreate)
    - [Update](#bookUpdate)
    - [Delete](#bookDelete)
  - [Categories](#categories)
    - [Index](#categoriesIndex)
    - [Show](#categoriesShow)
    - [Create](#categoriesCreate)
    - [Update](#categoriesUpdate)
    - [Delete](#categoriesDelete)
  - [Authors](#authors)
    - [Index](#authorsIndex)
    - [Show](#authorsShow)
    - [Create](#authorsCreate)
    - [Update](#authorsUpdate)
    - [Delete](#authorsDelete)
- [Validation](#validation)
- [Error Handling](#error-handling)
- [Entity Relation Diagram](#entity-relation-diagram)

## Installation
To set up the Widi Pustaka book management API, follow this steps:

1. Clone the repository:
```sh
git clone https://github.com/NymWidana/widi-pustaka.git
cd widi-pustaka
```

2. Install dependencies:
```sh
composer install
```

3. Copy the environment file and configure the anvironment variables:
```sh
cp .env.example .env
```
Update the `env` file with your database credentials and other necessary configuration.

4. Generate an application key:
```sh
php artisan key:generate
```

5. Run the database migrations and seeder
```sh
php artisan migrate --seed
```

6. Start the development server:
```sh
php artisan serve
```

## Configuration
Ensure that the folowing environment variables is configured in your `.env` file correctly:
- `DB_DATABASE`
- `DB_USERNAME`
- `DB_PASSWORD`

## API Endpoints
### Books
- __<h4 id="booksIndex">Get All Books</h4>__
    
    __Endpoint__
    ```http
    GET /api/books
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/books
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": [
                {
                    "id": 1,
                    "title": "Open-source nextgeneration application",
                    "description": "Perspiciatis sapiente rerum mollitia aut dicta. Dolorum eos id tenetur repellendus.",
                    "created_at": "2025-02-20T11:20:46.000000Z",
                    "updated_at": "2025-02-20T11:20:46.000000Z",
                    "author_ids": [
                        31,
                        4
                    ],
                    "category_ids": [
                        32,
                        39,
                        30,
                        58
                    ]
                },
                {
                    "id": 2,
                    "title": "Centralized well-modulated internetsolution",
                    "description": "Aperiam iusto illo minima et nesciunt sint non. Harum ratione voluptas sed incidunt.",
                    "created_at": "2025-02-20T11:20:46.000000Z",
                    "updated_at": "2025-02-20T11:20:46.000000Z",
                    "author_ids": [
                        32
                    ],
                    "category_ids": [
                        3,
                        61,
                        69
                    ]
                },
                {
                    "id": 3,
                    "title": "Multi-layered client-driven flexibility",
                    "description": "Corporis ut et quasi doloribus. Voluptate corporis dolores ut ut quidem.",
                    "created_at": "2025-02-20T11:20:46.000000Z",
                    "updated_at": "2025-02-20T11:20:46.000000Z",
                    "author_ids": [
                        18
                    ],
                    "category_ids": [
                        37,
                        3,
                        52,
                        40
                    ]
                }
            ],
        "success": true,
        "message": "Successfully retrieved all books data!"
    }
    ```

- __<h4 id="booksShow">Get Book by ID</h4>__
    
    __Endpoint__
    ```http
    GET /api/books/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/books/1
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": {
            "id": 1,
            "title": "Open-source nextgeneration application",
            "description": "Perspiciatis sapiente rerum mollitia aut nihil accusamus dicta. Dolorum eos id tenetur repellendus.",
            "created_at": "2025-02-20T11:20:46.000000Z",
            "updated_at": "2025-02-20T11:20:46.000000Z",
            "author_ids": [
                31,
                4
            ],
            "category_ids": [
                32,
                39,
                30,
                58
            ]
        },
        "success": true,
        "message": "Successfully retrieved the book data!"
    }
    ```

- __<h4 id="booksCreate">Create Book</h4>__
    
    __Endpoint__
    ```http
    POST /api/books
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/books
    ```

    __Request Body Example__
    ```json
    {
        "title" : "New Book",
        "description" : "Book Description",
        "categories" : [1, 2],
        "authors" : "Alan Turing"
    }
    ```

    __Response Example__
    ```json
    {
        "code": 201,
        "data": {
            "id": 101,
            "title": "New Book",
            "description": "Book Description",
            "created_at": "2025-02-20T11:35:25.000000Z",
            "updated_at": "2025-02-20T11:35:25.000000Z",
            "author_ids": [
                51
            ],
            "category_ids": [
                1,
                2
            ]
        },
        "success": true,
        "message": "Successfully saved a book data!"
    }
    ```

- __<h4 id="booksUpdate">Update Book</h4>__
    
    __Endpoint__
    ```http
    PUT /api/books/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/books/101
    ```

    __Request Body Example__
    ```json
    {
        "title" : "Updated Book",
        "description" : "Updated Book Description",
        "categories" : [1, 2, 3],
        "authors" : ["Alan Turing", "Albert Einstein"]
    }
    ```

    __Response Example__
    ```json
    {
        "code": 201,
        "data": {
            "id": 101,
            "title": "Updated Book",
            "description": "Updated Book Description",
            "created_at": "2025-02-20T11:35:25.000000Z",
            "updated_at": "2025-02-20T11:41:57.000000Z",
            "author_ids": [
                51,
                52
            ],
            "category_ids": [
                1,
                2,
                3
            ]
        },
        "success": true,
        "message": "Successfully updated a book data!"
    }
    ```

- __<h4 id="booksDelete">Delete Book</h4>__
    
    __Endpoint__
    ```http
    DELETE /api/books/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/books/101
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": {
            "id": 101,
            "title": "Updated Book",
            "description": "Updated Book Description",
            "created_at": "2025-02-20T11:35:25.000000Z",
            "updated_at": "2025-02-20T11:41:57.000000Z",
            "author_ids": [
                51,
                52
            ],
            "category_ids": [
                1,
                2,
                3
            ]
        },
        "success": true,
        "message": "Successfully deleted a book data!"
    }
    ```

### Categories
- __<h4 id="categoriesIndex">Get All Categories</h4>__
    
    __Endpoint__
    ```http
    GET /api/categories
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/categories
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": [
            {
                "id": 1,
                "name": "Fiction",
                "created_at": "2025-02-20T11:20:45.000000Z",
                "updated_at": "2025-02-20T11:20:45.000000Z",
                "book_ids": [
                    30,
                    35,
                    80,
                    84
                ]
            },
            {
                "id": 2,
                "name": "Mystery",
                "created_at": "2025-02-20T11:20:45.000000Z",
                "updated_at": "2025-02-20T11:20:45.000000Z",
                "book_ids": [
                    12,
                    75
                ]
            },
            {
                "id": 3,
                "name": "Science Fiction",
                "created_at": "2025-02-20T11:20:45.000000Z",
                "updated_at": "2025-02-20T11:20:45.000000Z",
                "book_ids": [
                    2,
                    3,
                    80,
                    94
                ]
            }
        ],
        "success": true,
        "message": "Successfully retrieved all categories data!"
    }
    ```

- __<h4 id="categoriesShow">Get Category by ID</h4>__
    
    __Endpoint__
    ```http
    GET /api/categories/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/categories/1
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": {
            "id": 1,
            "name": "Fiction",
            "created_at": "2025-02-20T11:20:45.000000Z",
            "updated_at": "2025-02-20T11:20:45.000000Z",
            "book_ids": [
                30,
                35,
                80,
                84
            ]
        },
        "success": true,
        "message": "Successfully retrieved the category data!"
    }
    ```

- __<h4 id="categoriesCreate">Create Category</h4>__
    
    __Endpoint__
    ```http
    POST /api/categories
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/categories
    ```

    __Request Body Example__
    ```json
    {
        "name" : "New Category"
    }
    ```

    __Response Example__
    ```json
    {
        "code": 201,
        "data": {
            "id": 71,
            "name": "New Category",
            "created_at": "2025-02-20T12:21:30.000000Z",
            "updated_at": "2025-02-20T12:21:30.000000Z",
            "book_ids": []
        },
        "success": true,
        "message": "Successfully saved a category data!"
    }
    ```

- __<h4 id="categoriesUpdate">Update Category</h4>__
    
    __Endpoint__
    ```http
    PUT /api/categories/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/categories/71
    ```

    __Request Body Example__
    ```json
    {
        "name" : "Updated Category"
    }
    ```

    __Response Example__
    ```json
    {
        "code": 201,
        "data": {
            "id": 71,
            "name": "Updated Category",
            "created_at": "2025-02-20T12:21:30.000000Z",
            "updated_at": "2025-02-20T12:23:13.000000Z",
            "book_ids": []
        },
        "success": true,
        "message": "Successfully updated a category data!"
    }
    ```

- __<h4 id="categoriesDelete">Delete Category</h4>__
    
    __Endpoint__
    ```http
    DELETE /api/categories/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/categories/71
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": {
            "id": 71,
            "name": "Updated Category",
            "created_at": "2025-02-20T12:21:30.000000Z",
            "updated_at": "2025-02-20T12:23:13.000000Z",
            "book_ids": []
        },
        "success": true,
        "message": "Successfully deleted a category data!"
    }
    ```

### authors
- __<h4 id="authorsIndex">Get All Authors</h4>__
    
    __Endpoint__
    ```http
    GET /api/authors
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/authors
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": [
            {
                "id": 1,
                "name": "Melody Terry",
                "created_at": "2025-02-20T11:20:46.000000Z",
                "updated_at": "2025-02-20T11:20:46.000000Z",
                "book_ids": [
                    38,
                    55,
                    90
                ]
            },
            {
                "id": 2,
                "name": "Jayde Jacobs",
                "created_at": "2025-02-20T11:20:46.000000Z",
                "updated_at": "2025-02-20T11:20:46.000000Z",
                "book_ids": [
                    7,
                    26,
                    27,
                    77,
                    91
                ]
            },
            {
                "id": 3,
                "name": "Lenora Bosco",
                "created_at": "2025-02-20T11:20:46.000000Z",
                "updated_at": "2025-02-20T11:20:46.000000Z",
                "book_ids": [
                    22,
                    30,
                    50,
                    71
                ]
            }
        ],
        "success": true,
        "message": "Successfully retrieved all authors data!"
    }
    ```

- __<h4 id="authorsShow">Get Author by ID</h4>__
    
    __Endpoint__
    ```http
    GET /api/authors/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/authors/1
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": {
            "id": 1,
            "name": "Melody Terry",
            "created_at": "2025-02-20T11:20:46.000000Z",
            "updated_at": "2025-02-20T11:20:46.000000Z",
            "book_ids": [
                38,
                55,
                90
            ]
        },
        "success": true,
        "message": "Successfully retrieved the author data!"
    }
    ```

- __<h4 id="authorsCreate">Create Author</h4>__
    
    __Endpoint__
    ```http
    POST /api/authors
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/authors
    ```

    __Request Body Example__
    ```json
    {
        "name" : "New Author"
    }
    ```

    __Response Example__
    ```json
    {
        "code": 201,
        "data": {
            "id": 53,
            "name": "New Author",
            "created_at": "2025-02-20T12:35:38.000000Z",
            "updated_at": "2025-02-20T12:35:38.000000Z",
            "book_ids": []
        },
        "success": true,
        "message": "Successfully saved an author data!"
    }
    ```

- __<h4 id="authorsUpdate">Update Author</h4>__
    
    __Endpoint__
    ```http
    PUT /api/authors/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/authors/53
    ```

    __Request Body Example__
    ```json
    {
        "name" : "Updated Author"
    }
    ```

    __Response Example__
    ```json
    {
        "code": 201,
        "data": {
            "id": 53,
            "name": "Updated Author",
            "created_at": "2025-02-20T12:35:38.000000Z",
            "updated_at": "2025-02-20T12:36:54.000000Z",
            "book_ids": []
        },
        "success": true,
        "message": "Successfully updated an author data!"
    }
    ```

- __<h4 id="authorsDelete">Delete Author</h4>__
    
    __Endpoint__
    ```http
    DELETE /api/authors/{id}
    ```

    __Request URL Example__
    ```http
    http://localhost:8000/api/authors/53
    ```

    __Response Example__
    ```json
    {
        "code": 200,
        "data": {
            "id": 53,
            "name": "Updated Author",
            "created_at": "2025-02-20T12:35:38.000000Z",
            "updated_at": "2025-02-20T12:36:54.000000Z",
            "book_ids": []
        },
        "success": true,
        "message": "Successfully deleted an author data!"
    }
    ```

## Validation
Widi Pustaka uses Laravel's validation mecanism. Here are the validation rules for creating a new book and updating a book:

___File:___ `app/Http/Requests/StoreBookRequest.php` and `app/Http/Requests/UpdateBookRequest.php`

```php
    public function rules(): array
    {
        return [
            'title' => 'required|string|max:255',
            'description' => 'string',
            'categories' => 'array',
            'categories.*' => 'integer|exists:categories,id',
            'authors' => [
                'required',
                'array',
                new NotEmptyArray
            ],
            'author.*' => 'string'
        ];
    }
```
---

The NotEmptyArray is a simple custom rule to check if the inputed array is empty

___File:___ `app/Rules/NotEmptyArray.php`

```php
    public function validate(string $attribute, mixed $value, Closure $fail): void
    {
        if (is_array($value) && empty($value)) {
            $fail('The book '.$attribute.' array must not be empty');
        }
    }
```
---
Book author field can be filled with array of string or string  of author name by:
- Makes sure intended string data is turned into array
- If its not string it will go to the validation rule 'array', if it isn't array it will fail
- If its array of non string value, it will not pass the validation rule 'string' of 'author.*'

___File:___ `app/Http/Requests/StoreBookRequest.php` and `app/Http/Requests/UpdateBookRequest.php`

___Method:___ `prepareForValidation`  
```php
    $authors = $this->input('authors');
    if (is_string($authors)) {
        $this->merge([
            'authors' => [$authors]
        ]);
    }
```
---
Book category field can be filled with array of integer or integer of category id by:
- Makes sure intended integer data is turned into array
- If its not integer it will go to the validation rule 'array', if it isn't array it will fail
- If its array of non integer value, it will not pass the validation rule 'integer'  of 'category.*' 

___File:___ `app/Http/Requests/StoreBookRequest.php` and `app/Http/Requests/UpdateBookRequest.php`

___Method:___ `prepareForValidation`  
```php
    $categories = $this->input('categories');
    if (is_int($categories)) {
        $this->merge([
            'categories' => [$categories]
        ]);
    }
```
---
Author and Category also have rules for creating and updating, for now all of them still just one simple string validation:

___File:___ `app/Http/Requests/StoreCategoryRequest.php`, `app/Http/Requests/UpdateCategoryRequest.php`, `app/Http/Requests/StoreAuthorRequest.php` and `app/Http/Requests/UpdateAuthorRequest.php`

```php
    public function rules(): array
    {
        return [
            'name' => 'string'
        ];
    }
```

## Entity Relation Diagram