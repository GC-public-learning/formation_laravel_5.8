
# dbsqlite

### using sqlite to manage db
1) make a .sqlite file in the database folder
2) modify ".env" file on the project root-> DB_CONNECTION=sqliteand delet the rest of DB params
3) modify "php.ini" file on your php folder and active the line  -> extension=pdo_sqlite
4) restart laragon
5) configure the migration on the laragon terminal ->
- php artisan migrate
- php artisan make:model Customer -m 
<br/>&emsp; 2 files created :
<br/>&emsp;- App/Models/Customer.php
<br/>&emsp;- database/migration/2021_05_16_073521_create_customers_table.php
<br/>&emsp;&emsp; modify this file and add rows you want to create on the "create place" ->
<br/>&emsp;&emsp;&emsp; - $table->string('name');
<br/>&emsp;&emsp;&emsp; - in the terminal -> php artisan migrate:refresh
5) use "Tinker" (test environement) in order to create records on the table created -> terminal -> php artisan tinker
<br/>&emsp;- $customer = new App\Models\Customer();
<br/>&emsp;- $customer->name = "Marc";
<br/>&emsp;- $customer->save();
<br/>&emsp;- $customer = new App\Models\Customer();
<br/>&emsp;- $customer->name = "Jean";
<br/>&emsp;- $customer->save();
<br/>&emsp;- App\Models\Customer::all();
<br/>&emsp; the console should be display the 2 created objects :
<br/>&emsp; <img src="https://github.com/Geoffrey-Carpentier/1st_laravel_project/blob/main/captures/tinker_display_created_customers.JPG" alt="capture customers" width="400">
<br/>&emsp;- exit;
6) modify the customers controller and the customers view to retrieve data from model correctly

created files :
----------------
[app/Models/](https://github.com/Geoffrey-Carpentier/1st_laravel_project/tree/main/app/Models)
<br/>&emsp;- [Customer.php](https://github.com/Geoffrey-Carpentier/1st_laravel_project/blob/6f6097c592cbb877a1129940c20061f5580aee3f/app/Models/Customer.php)
<br/><br/>[database/migrations/](https://github.com/Geoffrey-Carpentier/1st_laravel_project/tree/main/database/migrations)
<br/>&emsp;- [2021_05_16_073521_create_customers_table.php](https://github.com/Geoffrey-Carpentier/1st_laravel_project/blob/6f6097c592cbb877a1129940c20061f5580aee3f/database/migrations/2021_05_16_073521_create_customers_table.php)

modified files :
----------------
[app/Http/Controllers/](https://github.com/Geoffrey-Carpentier/1st_laravel_project/tree/main/app/Http/Controllers)
<br/>&emsp;- [CustomersController.php](https://github.com/Geoffrey-Carpentier/1st_laravel_project/blob/6f6097c592cbb877a1129940c20061f5580aee3f/app/Http/Controllers/CustomersController.php)

<br/><br/>[resources/views/customers/](https://github.com/Geoffrey-Carpentier/1st_laravel_project/tree/main/resources/views/customers)
<br/>&emsp;- [index.blade.php](https://github.com/Geoffrey-Carpentier/1st_laravel_project/blob/6f6097c592cbb877a1129940c20061f5580aee3f/resources/views/customers/index.blade.php)
