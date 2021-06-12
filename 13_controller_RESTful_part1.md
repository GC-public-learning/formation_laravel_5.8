
# Controller RESTful part 1

### the goal :  

1) go to the controller documentation page from the Laravel site and look an eye on the array with
the differents actions available by the controller in order to modify our controller with more conventional ways
<img src="https://github.com/Geoffrey-Carpentier/formation_laravel_5.8/blob/main/img/array_controller_actions.JPG" alt="array controller actions" width="800">
2) rename the list() function on the controller by  index() :
~~~
public function index() {
~~~

3) rename the route that acces the hold list() function in web.php :
~~~
Route::get('customers', [CustomersController::class, 'index']);
~~~

4) create the acces on the create view on the CustomersController :
~~~
public function create() {
      return view('customers.create');
}
~~~

5) add new route on web.php for the create function
~~~
Route::get('customers/create', [CustomersController::class, 'create']);
~~~

6) make a link on the customer index towards the create page
~~~
<!--- use bootstrap class to make a button with the link with a margin of 3--->
<a href="/customers/create" class="btn btn-primary my-3">new customer</a>
~~~

7) modify the "create()" function from the CustomersController to handle the company model used by the form and delete 
the handling of companies on the "index()" function because we wont need it anymore:
~~~
public function index() {
  //$customers = Customer::all();

    // filtered request
    $customers = Customer::status();

 // compact is a convenient way to send data on the view
 return view('customers.index', compact('customers'));
}

public function create() {
    $companies = Company::all();
    return view('customers.create', compact('companies'));
}
~~~

8) make the create view for the customers : in the customers folders create "create.blade.php" and cut the form 
from the customers index inside it :
~~~
@extends('layout')
@section('content')
<h1>create customer</h1>

<form action="customers" method="POST">
	<!-- laravel tool to forbid csrf with a token -->
	@csrf
	<div class="form-group">
		<input type="text" class="form-control @error('name') is-invalid 
			@enderror" name="name" placeholder="name">
		@error('name')
		 <div class="invalid-feedback">
		 	<!-- return the error handled by the controller with the chosen rules  -->
      		{{ $errors->first('name')}}
   		 </div>
   		@enderror
   	</div>

	<div class="form-group">
		<input type="email" class="form-control @error('email') is-invalid 
			@enderror "name="email" placeholder="email">
		@error('email')
		 <div class="invalid-feedback">
      		{{ $errors->first('email')}}
   		 </div>
   		@enderror
	</div>

	<div class="form-group">
		<div class="form-check">
  			<input class="form-check-input" type="checkbox" name="status">
  			<label class="form-check-label">active ?</label>
		</div>
		<script>
			
		</script>
	</div>

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
  <br/>
	<button type="submit" class="btn btn-primary">add customer</button>	
</form>
@endsection

~~~

9) if you use the navigation bar to go in another view from the create page there will have an error because the
links from the layout dont have a slash on the beginning. So just add a slash on each link from the layout.and add 
a slash on the customers path in the form tag in the field "action"
~~~
<form action="/customers" method="POST">
<a class="nav-link" href="/customers">Customers</a>
<a class="nav-link" href="/contact">Contacts</a>
<a class="nav-link" href="/infos">Infos</a>
~~~

10) modify the variable $customers from in index() function from the CustomersController to retrieve all the client :
~~~
$customers = Customer::all();
~~~

11) copy a table model from Boostrap to display with a better way the customers in the "index" customer view :
~~~
@extends('layout')
@section('content')
<h1>Customers</h1>
<!--- use bootstrap class to make a button with the link with a margin of 3--->
<a href="/customers/create" class="btn btn-primary my-3">new customer</a>

<table class="table table-striped">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Status</th>
      <th scope="col">Company</th>
    </tr>
  </thead>
  <tbody>
  	@foreach($customers as $c)
    <tr>
      <th scope="row">{{$c->id}}</th>
      <td>{{$c->name}}</td>
      <td>{{$c->status}}</td>
      <td>{{$c->company->name}}</td>
    </tr>
    @endforeach
  </tbody>
</table>
@endsection
~~~

<br/> to show the status if there are only 2 values (boolean) you can use the ternary operator :
~~~
{{$c->status ? "active" : 'inactive'}}
~~~

12) add a getter for the status in the "customer" model to get the name of the status instead a number (to handle more than 2 values)
useless in this case because "status" is boolean. just use the ternary operator before in the view is enough :
~~~
public function getStatusAttribute($attributes) {
    return [
      False => 'inactive',
      True => 'active'
    ][$attributes];
}
~~~

modified & created files :
----------------
1 created files and 5 modified files : 


commits : 
https://github.com/Geoffrey-Carpentier/1st_laravel_project/commit/db7efbfb6fd96f7426f4080e54e515ba8ffbbc26
https://github.com/Geoffrey-Carpentier/1st_laravel_project/commit/59c8d9c1abf5434b412ec49d20dc416875896e22




