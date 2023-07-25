# Laravel-Vue-User-CRUD

# Getting started

## Installation

Clone the repository

    git clone https://github.com/priyankamackwan/User-CRUD-Laravel-Vue.git

Switch to the repo folder

    cd User-CRUD-Laravel-Vue

Install all the dependencies using composer

    composer install

Copy the example env file and make the required configuration changes in the .env file

    cp .env.example .env

Generate a new application key

    php artisan key:generate

Run the database migrations (**Set the database connection in .env before migrating**)

    php artisan migrate

Start the local development server

    php artisan serve

You can now access the server at http://localhost:8000

**TLDR command list**

    git clone https://github.com/priyankamackwan/User-CRUD-Laravel-Vue.git
    cd User-CRUD-Laravel-Vue
    composer install
    cp .env.example .env
    php artisan key:generate
    
**Make sure you set the correct database connection information before running the migrations**

    php artisan migrate
    php artisan serve

## Database seeding

**Populate the database with seed data with relationships which includes users, articles, comments, tags, favorites and follows. This can help you to quickly start testing the api or couple a frontend and start using it with ready content.**

Run the database seeder and you're done

    php artisan db:seed

***Note*** : It's recommended to have a clean database before seeding. You can refresh your migrations at any point to clean the database by running the following command

    php artisan migrate:refresh

## Environment variables

- `.env` - Environment variables can be set in this file

***Note*** : You can quickly set the database information and other variables in this file and have the application fully working.

----------

# Testing

Run the laravel development server

    php artisan serve

Can now be accessed at

    http://localhost:8000/
Live website URL

    http://localhost:8000/
