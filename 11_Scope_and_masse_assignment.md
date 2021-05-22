
# Scopeand mass assignement

the goal 

1) create a scope method in the "customer model class" to retrieve filtred data from the db
~~~
public function scopeStatus($query) {
    return $query->where('status', True)->get();
}
~~~
3) change the name of the nickname parameter on the view in order it correspond with the name from the table customer
4) use the array returned by the request validate method to directly insert date in the new created object (in the "method store()")
~~~
$customer = new Customer() and $customer->save() replaced by Customer::create($array);
~~~
- dont forget to add the status apart because it can be managed with the validate method (param of a check box exist or not)
4) modify the customer model to accept the new array
~~~
protected $fillable = ['name', 'email', 'status'];
~~~

modified files :
----------------

3 modified files : https://github.com/Geoffrey-Carpentier/1st_laravel_project/commit/6a040a296d71b8a259582bb464380aa328abb06a



