## Test Laravel Auth

there are PHPUnit tests in `tests/Feature/AuthenticationTest.php` file.


---

## Task 1. Routes Protected by Auth.

File `routes/web.php`: profile functionality URLs should be available only for logged-in users.

Test method `test_profile_routes_are_protected_from_public()`.

---

## Task 2. Link Visible to Logged-in Users.

File `resources/views/layouts/navigation.blade.php`: the "Profile" link should be visible only to logged-in users.

Test method `test_profile_link_is_invisible_in_public()`.

---

## Task 3. Profile Fields.

File `resources/views/auth/profile.blade.php`: replace "???" values for name/email with logged-in user's name/email.

Test method `test_profile_fields_are_visible()`.

---

## Task 4. Profile Update.

File `app/Http/Controllers/ProfileController.php`: fill in the method `update()` with the code to update the user's name and email.
If the password is filled in, also update that.

Test methods: `test_profile_name_email_update_successful()` and `test_profile_password_update_successful()`.

---

## Task 5. Email Verification.

Make the URL `/secretpage` available only to those who verified their email.
You need to make changes to two files.

In file `routes/web.php` add a Middleware to `/secretpage` URL.
And enable email verification in the `app/Models/User.php` file.

Test method: `test_email_can_be_verified()`.

---

## Task 6. Password Confirmation.

Make the URL `/verysecretpage` redirect to a page to re-enter their password once again.
In file `routes/web.php` add a Middleware to that URL.

Test method: `test_password_confirmation_page()`.

---

## Task 7. Password with Letters.

By default, registration form requires password with at least 8 characters.
Add a validation rule so that password must have at least one letter, no matter uppercase or lowercase.

So password `12345678` is invalid, but password `a12345678` is valid.

Hint: you need to modify file `app/Http/Controllers/Auth/RegisteredUserController.php`, which is almost default from Laravel Breeze.

Test method: `test_password_at_least_one_uppercase_lowercase_letter()`.

---


DB:
--

Copy the contents of your .env or .env.example file to create a file called .env.testing

Change the value of APP_ENV to 'testing'

remove all of the DB_ entries

Make sure your phpunit.xml has the following lines and uncomment them:

<env name="DB_CONNECTION" value="memory_testing"/>
<env name="DB_DATABASE" value=":memory:"/>

Add the following array to your connections in database.php:

'connections' => [

   'memory_testing' => [
     'driver' => 'sqlite',
     'database' => ':memory:',
     'prefix' => '',
   ],

   ...
Finally, run 
	php artisan optimize:clear
 to clear the caches.

Your unit and feature tests should now be using the in-memory SQLite database, 
while your local should continue using the database configured in .env file.



APP KEY:
--------

php artisan key:generate --env=testing



MySQL error key too long:
------------------------

Solution 1:

In file appServiceProvider.php in function boot() ->   Schema::defaultStringLength(191);

Solution 2:

Inside config/database.php, replace this line for mysql

'engine' => null',

with

'engine' => 'InnoDB ROW_FORMAT=DYNAMIC',


Then retry    php artisan migrate:fresh

