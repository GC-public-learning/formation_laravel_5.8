
# Controller RESTful part 2

### the goal : make the GET "/customers/{customer}" route and use "model binding"

1) Add new route in "web.php" from "routes/" :
~~~
// "customer" mean "id" of that last one
Route::get('customers/{customer}', [CustomersController::class, 'show']);
~~~
2) Add new method on "CustomersController.php" from "app/Http/Controllers/" with model binding:
~~~
/*
public function show($customer) { # $customer is an id
    # $customer = Customer::find($customer);

    # better than the instruction just above because generate 404 if error
    $customer = Customer::where('id', $customer)->firstOrFail();
    # dd($customer); # to test
    return view('customers.show', compact('customer'));
}
*/

// model binding : shorter way and generate automaticaly 404 in error case
public function show(Customer $customer) {
    return view('customers/show', compact('customer'));
}
~~~
3) modify the name cell from the array of customers in index.bade.php from "ressources/views/customers/" in order to make it linkable :
~~~
<td><a href="/customers/{{ $c->id}}">{{$c->name}}</a></td>
~~~
4) make the new "show.blade.php" view on "ressources/views/customers/" :
~~~
@extends('layout')
@section('content')
	<h1>{{ $customer->name }}</h1>
	<hr>
	<p><strong>Email :</strong> {{ $customer->email}}</p>
	<p><strong>Company :</strong> {{ $customer->company->name}}</p>
@endsection
~~~

