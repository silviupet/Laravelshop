Lectia 1

1. Logare github new repo Laravelshop
2. creare folder htdocs Laravelshop
3. terminal Pushd c:\xampp\htdocs\Laravelshop  

composer create-project laravel/laravel . "5.8.*" ia ultima versiune de laravel

4. urcare pe github 

se verifica daca .env este pus la gitignore 
git init
git add -A sau git add . 
git commit -m"mesaj"
git add origin master https://github.com/silviupet/Laravelshop.git
git push origin master

5. config virtual host optional

6. configurare dB creare dB (acelas numa ca si proiectul), privilegii add user 

7. configurare .env cu datele de conectare din db

8. Migrare

php artisan migrate

sau php artisan migrate:fresh  ( sterge db si creaza una noua -> nare atentie cu aceasta comanda  ca pierdem datele 

9. creare model 

php artisan make model Product -m  (m creaza si fisierul de migrare)

practic se creaza un model avand id si timestamp

deschidem fisierul de migrare (database/migration) si adaugam si celelalte campuri de care avem nevoie in db

10 migram fisierul de migrare 

php artisam migrate 

11.  mergem in app/providers/product.php si adaugam campurile care vor fi editate 

protected $fillable = [
        'name',
        'description',
        'photo',
        'price'
    ];

daca nu facem acest lucru ne va da eroare cand completam campurile

12. daca vrem sa adaugam ceva in db:  -  seed
 
php artisan make:seed ProductSeeder
genereaza un fisier seed  ->pt testare . 
se completeaza acel fisier cu date s-a luat de pe github si s-a adaugar in public function run 

php artisan db:seed --class=ProductSeeder

12 controller
php artisan make:controller ProductsController --resource

--resource creaza automat clasele index, create, show, update destroy

 13 editare fisierul de rute routes /web php  adaugare Route::resource('products', 'ProductsController');

14 partea de view
layout p pt fiec categ de produse pot folosi un layout
pt fiecare metoda din controller pot folosi un view de preferat (index.blade.php, create .blade.php etc_ 
in view putem face un folder Products  si aici fisierele de mai sus +layour.blade.php  
@extends('products.layout') bucatica de cod care urmeaza sa extinda layoutul din folderul products
@section ('content')
..
@end section 
 extinde si pune sectiunea contents  - in layout.blade.php avem  @yield('content')
practic incarc continut html in alt continut html (layoutul are header, sidebar,footer iar mainpage este dinamic )

15 ProductsController se completeaza metodele

16. CSS din assets 

17 la Create  se face un request de tip POST scre se duce in met store si aici ar trebui sa avem o validare 

request()->validate([
            'name' => 'required',
            'description' => 'required',
            'price' => 'required',
        ]);
        $file = $request->file('photo');
        if(!empty($file)) {
            $imageName = time().'.'.$file->getClientOriginalExtension();
            $file->move(public_path('images'), $imageName);



Lectia 2 



##Install composer (for dependency management)

curl -sS https://getcomposer.org/installer | php
 sudo mv composer.phar /usr/local/bin/composer
Install
Step 1.
mkdir Laravelshop
Step 2.
sudo chmod 644 -R Laravelshop doar pt mac
Step 3.
cd Laravelshop
Step 4. Daca vrei sa dawnladezi de pe github Download the master branch
git clone https://github.com/aadiaconitei/laravelshop.git .
Step 5. Make sure you have a database :Laravelshop
Step 6. Make a copy .env.example and rename to .env and edit lines 12,13,14:
din terminal cp .env.example .env
ls -all
deschid env
vi .env
editam linile 12,13,14
esc wq ->pt save

DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret
Step 7. Install the composer dependencies
composer install
or

php /usr/local/bin/composer.phar
Step 8. Run the migrations and seeds
php artisan migrate --seed
or

php artisan migrate
php artisan db:seed
The db:seed command will seed admin and settings table. If you want to pre-generate some mock data, run again with option --class=ProductsSeeder

Step 9.
chmod -R 755 storage
chmod -R 755 bootstrap/cache
Step 10. Generating the key doar daca e downloadat de pe github tr generata o cheie de securitate
php artisan key:generate
[Optional:] php artisan cache:clear php artisan config:clear

Step 11.
http://localhost/Laravelshop/public/
http://localhost/Laravelshop/public/products/listProducts
Authentication
php artisan make:auth

 public  function __construct()
    {
      /*$this->middleware('auth');
        /*
         * $this->middleware('auth');  //toate metodele pot fi accesate doar logat
         */
         /*
         * $this->middleware('auth', ['only' => ['create', 'store', 'edit', 'delete']]);//lista de metode ce pot fi accesate doar logat
         */
         /*
          * $this->middleware('auth', ['except' => ['cart', 'listProducts','updateCart', 'addToCart']]); //lista de metode ce pot fi accesate nelogat
          */
You can type the route:list command to see all routes registered by your application:

php artisan route:list



##REST api

Step 1. I created new folder “API” in App\Http\Controllers folder
mkdir app/API

Step 2. Create new controller as APIBaseController and ProductAPIController, APIBaseController extend all api controller (not include the create or edit methods)
 php artisan make:controller API/ProductAPIController --api
 php artisan make:controller API/APIBaseController --api 
Step 3. Create resource routes for list, create, update and delete. so we open your routes/api.php file and put the code following api.php: routes/api.php
Route::resource('apiproducts', 'API\ProductAPIController');
Step 4. Postman requests
List: GET, URL:http://localhost/laravelshop/public/api/apiproducts

Create: POST, URL:http://localhost/laravelshop/public/api/apiproducts

Show: GET, URL:http://localhost/laravelshop/public/api/apiproducts/{id}

Update: PUT, URL:http://localhost/laravelshop/public/api/apiproducts/{id}

Delete: DELETE, URL: http://localhost/laravelshop/public/api/apiproducts/{id}



<p align="center"><img src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</p>

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains over 1400 video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

## Laravel Sponsors

We would like to extend our thanks to the following sponsors for funding Laravel development. If you are interested in becoming a sponsor, please visit the Laravel [Patreon page](https://patreon.com/taylorotwell).

- **[Vehikl](https://vehikl.com/)**
- **[Tighten Co.](https://tighten.co)**
- **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
- **[64 Robots](https://64robots.com)**
- **[Cubet Techno Labs](https://cubettech.com)**
- **[Cyber-Duck](https://cyber-duck.co.uk)**
- **[British Software Development](https://www.britishsoftware.co)**
- **[Webdock, Fast VPS Hosting](https://www.webdock.io/en)**
- **[DevSquad](https://devsquad.com)**
- [UserInsights](https://userinsights.com)
- [Fragrantica](https://www.fragrantica.com)
- [SOFTonSOFA](https://softonsofa.com/)
- [User10](https://user10.com)
- [Soumettre.fr](https://soumettre.fr/)
- [CodeBrisk](https://codebrisk.com)
- [1Forge](https://1forge.com)
- [TECPRESSO](https://tecpresso.co.jp/)
- [Runtime Converter](http://runtimeconverter.com/)
- [WebL'Agence](https://weblagence.com/)
- [Invoice Ninja](https://www.invoiceninja.com)
- [iMi digital](https://www.imi-digital.de/)
- [Earthlink](https://www.earthlink.ro/)
- [Steadfast Collective](https://steadfastcollective.com/)
- [We Are The Robots Inc.](https://watr.mx/)
- [Understand.io](https://www.understand.io/)
- [Abdel Elrafa](https://abdelelrafa.com)
- [Hyper Host](https://hyper.host)

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-source software licensed under the [MIT license](https://opensource.org/licenses/MIT).
"# Laravelshop" 
