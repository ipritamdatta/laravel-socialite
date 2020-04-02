http://computerengineeringfree4u.xyz/how-to-add-google-login-in-laravel-6-0/

How to Add google login in Laravel 6 0
====================================
1. Install project 
 composer create-project --prefer-dist laravel/laravel google_login
2. Setup a MySQL database
 configure the database in the .env file.
  DB_CONNECTION=mysql
  DB_HOST=127.0.0.1
  DB_PORT=3306
  DB_DATABASE=laravelgoogle
  DB_USERNAME=root
  DB_PASSWORD=
3. Add field in user migrations
 field name name id google_id  
   
4. Run  migrations command
 php artisan migrate
5. Create a Laravel Authentication
 in Laravel 6.0 you can not run php artisan make:auth.
 first You can install the laravel/ui package via composer
  composer require laravel/ui
  php artisan ui vue --auth
  npm install 
  npm run dev
    After run this command you can see build is mix notification. 
    After show this notification refresh page 
6. Download the laravel/socialite package for laravel google integration    
 composer require laravel/socialite
  Locate the providers in config  app.php file and register the SocialiteServiceProvider.
              
     Laravel\Socialite\SocialiteServiceProvider::class,           

  Spot the aliases in config  app.php file and register the aliases.

          'Socialite' Laravel\Socialite\Facades\Socialite::class,
         
7. Create Google App To Get Tokens
 if project not created project then showing 
   OAuth consent screen
   in this screen fill 
    Application name = your App name 
    Application logo = upload you website logo
    Authorised domains = Add Your domains name
    Application Privacy Policy link = Add Policy Privacy Link you can genrate online free 
    After fill this data and save 
 Go to the Google’s developers portal by following URL: https://console.developers.google.com
 Login via your Gmail account. You will see something like this.
 Shortly you have to click on Create Application.  After generated application you can see the following slide:
 In above image, you can see Client ID and Client Secret, which we need in our Laravel Application.
8. Add in config.services.php  
  'google' = [
        'client_id' = 'xxxx', // your client_id form google console
        'client_secret' = 'xxxx', // your client_secret form google console
        'redirect' = 'http://localhost:8000/callback'],
9. Generate a controller
 use following command 
  *php artisan make:controller SocialAuthGoogleController*
  use Illuminate\Http\Request; 
  use App\User;
  use Socialite;
  use Auth; 
  use Exception;
 We must implement two methods in this controller, which are following.
  1)redirect():  Redirect our users to the Google.
       

  2) callback():  Handle callback from Google. 
  
10. add in a view page
  a href="{{ url('/redirect') }}" class="btn btn-primary" Login With Google /a     
11. add routes in web.php
 Route::get('/redirect', 'SocialAuthGoogleController@redirect');
 Route::get('/callback', 'SocialAuthGoogleController@callback');
12.start laravel project 
   Php artisan serve
