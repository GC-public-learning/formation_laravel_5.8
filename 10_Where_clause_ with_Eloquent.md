
Where clause with Eloquent 

the goal is to define a status for each customer in order to get a list of customers filtred by status.

1) add a new line in the "create customers tabble from the migration folder to integer the new row status
2) as always in the Laragon terminal tape the command : php artisan:migrate refresh;
3) modify the associate controler to integer the new value
4) modify the list() controller method to get a filtred by status result from the customer table
5) modify the view linked to the form to integer the new status value 

modified files :
----------------

2 modified files :

https://github.com/Geoffrey-Carpentier/1st_laravel_project/commit/a3799c431cc9ba8f6022b09bb120da347687e82e


