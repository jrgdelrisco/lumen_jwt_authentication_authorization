# Step by step guide

This is a small project I made that uses Lumen, firebase/php-jwt library for authentication and authorization through middleware, database migrations and seeding. I let you bellow the steps you have to take to get running a project like this one.

## Prerequisites

1. Install Wamp and you're done (I'm using Windows 10)
2. Text editor of your choice (VSCode)

## Steps

1. Run the command:

    > composer create-project laravel/lumen the_project_name

2. Go inside generated folder:

    > cd the_project_name

3. Make a copy of .env.example (if doesn't exists):

    > cp .env.example .env

4. For the APP_KEY and JWT_SECRET values you can generate those with the following command inside the project's folder:

    > php -r "require 'vendor/autoload.php'; echo str_random(32).PHP_EOL;"

5. Make a migration for users' database table:

    > php artisan make:migration create_users_table

6. See generated file in migrations folder

7. Create a factory method that will help us in populating some seed data in the database. See database/factories/ModelFactory.php file

8. Create the seeder with the following command:

    > php artisan make:seeder UsersTableSeeder

9. Modify the file database/seeds/UsersTableSeeder.php

10. Register this user seeder in our database seeders. See database/seeds/DatabaseSeeder.php file

11. Go to phpMyAdmin and create the database "the_project" (DB_DATABASE), with user name "project_user" (DB_USERNAME), and generate password (DB_PASSWORD) too. Set these three data into the .env configuration file. My variable DB_PORT=3307 because I'm using Wamp with MariaDB

13. Register AppServiceProvider in bootstrapp/app.php file (uncomment corresponding line). Uncomment Facades and Eloquent related lines too

14. Modify the file app/Providers/AppServiceProvider.php (for innodb_large_prefix option)

15. Create database:
    > php artisan migrate

16. Seed database:
    > php artisan db:seed

17. Install firebase/php-jwt library:

    > composer require firebase/php-jwt

18. Create login route. See routes/web.php file

19. Create controller. See app/Http/Controllers/AuthController.php file

20. Create Authorization middleware. See app/Http/Middleware/AuthMiddleware.php file

21. Register AuthMiddleware and set an alias in bootstrap/app.php file

22. Protect some routes with our middleware. See routes/web.php

23. Play with Postman:

    > php -S localhost:8000 -t .\public\

    > POST: http://localhost:8000/auth/login    
    > Body: {"login":"user_from_database_or_email","dumbpassword":"user_password"}
    > Headers: Content-Type application/json

    then

    > GET: http://localhost:8000/users
    > Headers: Authorization token_value

