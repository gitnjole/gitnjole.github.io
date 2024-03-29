---
layout: page
title: Simple MVC
description: a barebones MVC framework
img: assets/img/projects/logo-color.png
importance: 1
category: Core PHP
---
{% raw %}

SimpleMVC is a lightweight custom PHP framework designed to provide a solid foundation for building robust web applications. This framework is mainly used for education purposes and as a learning tool, built to closely resemble the Laravel framework. 

## Current version
```
0.3.6
```
## Features

- **MVC Architecture:** Follows the Model-View-Controller architectural pattern for organized and maintainable code.
- **Routing:** Clean and customizable URL routing for handling requests.
- **Database Support:** Supports database integration and connections. Tested using MySQL and PostgreSQL. With some tweaks can work with most DMBS.
- **Template and Layout Engine:** Includes a simple and efficient template engine for building dynamic views. Can also use multiple layouts for different devices/parts of website.
- **Middleware Support:** Easily implement middleware for processing HTTP requests and responses.
- **Error Handling:** Comprehensive error handling for debugging and logging.

## Working:

>- [x] Router.
>- [x] Handle POST data.
>- [x] Handle GET data.
>- [X] Handle user registration.
>- [x] Layouts.
>- [x] Validation.
>- [x] Models.
>- [x] Middleware.
>- [X] Database connection.

## Known issues:

At this point in the project, many. Notable known issues will be posted here.

## Installation

1. Clone archive using git
```bash
git clone https://github.com/gitnjole/simple-mvc
```
2. Modify the database schema in `migrations/`
3. Create `.env` file from `.env-example` and adjust database parameters
4. Run `composer install`
5. Run migrations by executing `php migrations.php` from the project root directory
6. Start the php server from the `web/` directory using
```bash
php -S 127.0.0.1:[desired_port]
```

# Getting started

## Routing

Define your routes in `web/index.php`.
```php
$app->router->get('/form', [SiteController::class, 'form']);
$app->router->post('/form', [SiteController::class, 'formHandler']);
```

## Controllers

Create controllers in `controllers/`.
```php
namespace app\controllers

class YourController extends Controller
{}
```

## Views

Create the views in `views/`.

Currently, views are embeded through `{{content}}` in `views/layouts/main.html`.

{% endraw %}
