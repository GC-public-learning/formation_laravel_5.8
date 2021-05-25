
# BelongsTo & HasMany

### the goal :  create severals models and manage relations betweens them

1) create a new model "Company" with its migration file , open laragon terminal :
~~~
php artisan make:model Company -m
~~~
2) add rows on the new table by adding line on the new migration file "create compagnies..."
~~~
 public function up()
    {
        Schema::create('companies', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
~~~
3) reset bdd, on terminal (rollback and recreate tables) :
~~~
php artisan migrate:refresh
~~~
replace the line in your Customer model to allow every data (not conventional)
~~~
protected $fillable = ['name', 'email', 'status'];
~~~
by
~~~
protected $guarded = [];
~~~
add the same line in the Company model :
~~~
class Company extends Model
{
    protected $guarded = [];
    //use HasFactory;
}
~~~

4) use tinker to create manually new companies in order to test the new configuration
<br/>&emsp; in the terminal :
~~~
php artisan tinker
App\Models\Company::create(['name' => 'My new company'])
App\Models\Company::create(['name' => 'My new company 2'])
~~~
5) go to the laravel Eloquent: Relationships web page to get the code to create new realtionships
<br>("one to many") because you want each company has many customers and one customer is attached on one company
<br> copy the comments method and place it on the model "Company" and modify it:
~~~
<?php

use App\Models\Customer;
namespace App\Models;


//use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Company extends Model {
    protected $guarded = [];
    //use HasFactory;
    public function customers() {
        return $this->hasMany(Customer::class);
    }
}

~~~
6) copy the "post"method from the same page into your customer model this case and modify it in order to retrieve
the company attached to the client :
~~~
<?php

use App\Models\Company;
namespace App\Models;

//use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Customer extends Model {
	// configure  the model to retrieve an array with data on his construction
	//protected $fillable = ['name', 'email', 'status'];

	// allow everything, not conventional but convenient for the training
	protected $guarded = [];
    //use HasFactory;

    public function scopeStatus($query) {
    	return $query->where('status', True)->get();
    }
     public function company() {
    	return $this->belongsTo(Company::class);
    }
}

~~~
7) add the foreign key on the "customers" table by adding new line on the create method from
 "create customers migration file
in terminal :
~~~
$table->unsignedInteger('company_id');
~~~
8) modify the customers view to display new infos
- add a form-select with error handling to select the companies
~~~
<div class="form-group">
		<select class="form-select @error('company_id') is-invalid 
			@enderror "name="company_id" aria-label="Default select example" 
			name="entreprise_id">
			@foreach($companies as $c)
		  		<option value="{{ $c->id}}">{{$c->name}}</option>
		 	@endforeach
		</select>
		@error('company_id')
		<div class="invalid-feedback">
      	{{ $errors->first('company_id')}}
   	</div>
   	@enderror
</div>
~~~
9) modify the "list" method from the customers controller to handle the new data :
~~~
 public function list() {
    // filtered request
    $customers = Customer::status();
    $companies = Company::all();

	   // compact is a convenient way to send data on the view
    return view('customers.index', compact('customers','companies'));
    }
~~~
10) recreate manually companies records with tinker because the "refresh" before has ereased all the data in the db

11) go to the "customers" controller and add new rule for the company id in the "store" function :
~~~
'company_id' => 'required|integer'
~~~
12) create severals clients with the form on the customer view to test if everything is alright

13) modify the view to display the company name instead of the email
~~~
<li>{{$c->name}} <em class="text-muted">{{$c->company->name}}</em></li>
~~~

modified & created files :
----------------
2 created files and 4 modified files : 

5 modified files because methods that call the controllers has been rewritten by new conventional way in the web.php from the "routes" folder :

~~~
Route::get('customers', 'App\Http\Controllers\CustomersController@list');
Route::post('customers', 'App\Http\Controllers\CustomersController@store');
~~~
replaced by 
~~~
Route::get('customers', [CustomersController::class, 'list']);
Route::post('customers', [CustomersController::class, 'store']);
~~~

dont forget to add the path on the CustomersController in a use function :
~~~
use App\Http\Controllers\CustomersController;
~~~

commit : https://github.com/Geoffrey-Carpentier/1st_laravel_project/commit/c344be1e152090602fd56eb6b8d50a199460d950




