# Controller RESTful part 3

### the goal :
### make the PATCH "customers/{customer}" route and use "model binding"
### make the GET "customers/{customer}/edit" route
### DELETE to finish....

1) cut this content on "create.blade.ph" from "views/customers/" and replace it by "@include('includes.form') :
~~~
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
~~~
2) create a new view "form.blade.php" in a new folder "views/customers/includes/" and paste the code cut
3) juste after the "h1" tag in "show.blade.php" add new link to edit the customers :
~~~
<a href="/customers/{{ $customer->id }}/edit" class="btn btn-secondary my-3">Edit</a>
~~~
4) create "edit.blade.php in "views/customers" :
~~~
@extends('layout')
@section('content')
<h1>Edit {{ $customer->name }}'s profile</h1>

<form action="/customers/{{ $customer->id }}" method="POST">
	<!-- laravel tool to forbid csrf with a token -->
	@method('PATCH')
	@include('/customers/includes.form')
	<button type="submit" class="btn btn-primary">Save infos</button>	
</form>
@endsection

~~~
5) on "web.php from "routes/" add new url to edit :
~~~
Route::get('customers/{customer}/edit', [CustomersController::class, 'edit'])
~~~
6) add "edit function" on the "CustomersController.php" from "app/Http/Controllers/" :
~~~
public function edit(Customer $customer) {
      $companies = Company::all();
      return view('customers/edit', compact('customer', 'companies'));
  }
~~~
7) on "form.blade.php" modify the fields to show the customers infos in case of a "edit"
and keep the inserted values in case of error in the same time :
~~~
<input type="text" class="form-control @error('name') is-invalid 
			@enderror" name="name" placeholder="name" value="{{ old('name') }} ?? {{ $customer->name }}">
<input type="email" class="form-control @error('email') is-invalid 
			@enderror "name="email" placeholder="email" value="{{ old('email') }} ?? {{ $customer->email }}">
<input class="form-check-input" type="checkbox" name="status" {{ $customer->status == 'active' ? 'checked' : '' }}>
<option value="{{ $c->id}}" {{ $customer->company_id == $c->id ? 'selected' : ''}}>{{$c->name}}</option>
~~~
8) on "web.php from "routes/" add new url to update :
~~~
Route::patch('customers/{customer}' [CustomersController::class, 'update']);)
~~~
9) add "update function" on the "CustomersController.php" from "app/Http/Controllers/" :
~~~
public function update(Customer $customer) {
    $data = request()->validate([
        'name' => 'required|min:3',
        'email' => 'required|email', # rules combination
        'company_id' => 'required|integer'
    ]);
    $customer->update($data);
    return redirect('/customers/'.$customer->id);

}
~~~
10) send an empty "Customer" object on the "create()" function from "CustomersController.php" to prevent "undefined variable error" with create form :
~~~
public function create() {
    $companies = Company::all();

    # send empty object to prevent "undefined variable error" with create form 
    $customer = new Customer();
    return view('customers.create', compact('companies', 'customer'));
}
~~~
11) add default attributes on the customer model to prevent another error from the create form because attributes of empty objects aren't defined :
~~~
protected $attributes = [
  'status' = False;
];
~~~
12)...
