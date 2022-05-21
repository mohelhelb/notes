### Notes

#### Built-in function: sorted

A common technique for sorting data is based on indexes and named attributes:
~~~
# Input
employees = [("John", 32, 50000), ("Jane", 27, 60000), ("Sarah", 35, 50000), ("Michael", 45, 90000)]
sorted_employees = sorted(employees, key=lambda emp: emp[2], reverse=True)
print(employees)
print()
print(sorted_employees)
~~~
~~~
# Output
[('John', 32, 50000), ('Jane', 27, 60000), ('Sarah', 35, 50000), ('Michael', 45, 90000)]

[('Michael', 45, 90000), ('Jane', 27, 60000), ('John', 32, 50000), ('Sarah', 35, 50000)]
~~~
~~~
# Input
def criteria(emp):
    lname = emp.name.split(" ")[1]
    return lname

class Employee():
    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self.salary = salary

    def __repr__(self):
        return f"({self.name}, {self.age}, {self.salary})"

emp_1 = Employee("Carl Smith", 37, 90000)
emp_2 = Employee("Sarah Fox", 27, 70000)
emp_3 = Employee("John Biden", 32, 50000)
emp_4 = Employee("Sarah Smith", 29, 60000)
employees = [emp_1, emp_2, emp_3, emp_4]
s_employees = sorted(employees, key=criteria)
print(employees)
print()
print(s_employees)
~~~
~~~
# Output
[(Carl Smith, 37, 90000), (Sarah Fox, 27, 70000), (John Biden, 32, 50000), (Sarah Smith, 29, 60000)]

[(John Biden, 32, 50000), (Sarah Fox, 27, 70000), (Carl Smith, 37, 90000), (Sarah Smith, 29, 60000)]
~~~
The *operator* module provides a couple of useful functions when sorting data: *itemgetter* and *attrgetter*
~~~
# Input
from operator import itemgetter

employees = [("Carl Smith", 37, 90000), ("Sarah Fox", 27, 70000), ("John Biden", 32, 50000), ("Sarah Smith", 29, 60000)]
s_employees = sorted(employees, key=itemgetter(1))
print(employees)
print()
print(s_employees)
~~~
~~~
# Output
[('Carl Smith', 37, 90000), ('Sarah Fox', 27, 70000), ('John Biden', 32, 50000), ('Sarah Smith', 29, 60000)]

[('Sarah Fox', 27, 70000), ('Sarah Smith', 29, 60000), ('John Biden', 32, 50000), ('Carl Smith', 37, 90000)]
~~~
~~~
# Input
from operator import attrgetter

class Employee():
    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self.salary = salary

    def __repr__(self):
        return repr((self.name, self.age, self.salary))
    
emp_1 = Employee("Carl Smith", 37, 90000)
emp_2 = Employee("Sarah Fox", 27, 70000)
emp_3 = Employee("John Biden", 32, 50000)
emp_4 = Employee("Sarah Smith", 29, 60000)
employees = [emp_1, emp_2, emp_3, emp_4]
s_employees = sorted(employees, key=attrgetter("name"))
print(employees)
print()
print(s_employees)
~~~
~~~
# Output
[('Carl Smith', 37, 90000), ('Sarah Fox', 27, 70000), ('John Biden', 32, 50000), ('Sarah Smith', 29, 60000)]

[('Carl Smith', 37, 90000), ('John Biden', 32, 50000), ('Sarah Fox', 27, 70000), ('Sarah Smith', 29, 60000)]
~~~

---

Reference:

https://docs.python.org/3/howto/sorting.html#sortinghowto

---

#### Classes

pending

---

#### Decorators

Generally speaking, the syntax of a decorator function is as follows:
~~~
# Input
def decorator(func):
    def wrapper(\*args, \*\*kwargs):
        # Any number of statements
        # Execute func
        # Any number of statements
    return wrapper
~~~
The syntax of the decorator functions that take positional arguments are slightly different:
~~~
# Input
def decorator(\*args):
    def subdecorator(func):
        def wrapper(\*args, \*\*kwargs):
            # Any number of statements
            # Execute func
            # Any number of statements
        return wrapper
    return subdecorator
~~~

---

#### List Comprehensions

Unlike *for statements*, *list comprehensions* are not only more concise and readable, but they also prevent some side effects like:
~~~
# Input
nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
l = []
for num in nums:
    l.append(num*num)
print(l)
print(f"The num variable is still accessible; in fact, its value is {num}")
~~~
~~~
# Output
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
The num variable is still accessible; in fact, its value is 81.
~~~
~~~
# Input
nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
l = [num**2 for num in nums]
print(l)
print("The num variable is not accessible in the global scope.")
~~~
~~~
# Output
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
The num variable is not accessible in the global scope.
~~~
The expresions that are defined in *list comprehensions* can also be user-defined functions:
~~~
# Input
nums = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
def func(x):
    y = x**2 / 3
    return round(y, 1)
l = [func(num) for num in nums if num % 2 != 0]
print(l)
~~~
~~~
# Output
[0.3, 3.0, 8.3, 16.3, 27.0]
~~~

---

References:

https://docs.python.org/3/tutorial/datastructures.html?highlight=list%20comprehension#list-comprehensions

---

#### pip

Upgrade all the Python packages that are not up-to-date in a virtual python environment at once.
~~~
pip list --local --outdated --format freeze | gawk 'BEGIN{FS="=="}{printf $1"\n"}' | xargs pip install -U  2> /dev/null
~~~

---

Create the *requirements.txt* file.
~~~
pip freeze --all --local > requirements.txt
~~~
	
#### OOP principles

pending

#### Python scopes and Namespaces

The variables that follow the global statement are to be interpreted as globals.
~~~
# Input

def foo():
    global x, y
    x = 1
    y = 2
    z = 3
    print(f"Local Namespace (foo): {locals()}")
foo()
print(f"x: {globals()['x']}, y: {globals()['y']}")
~~~
~~~
# Output

Local Namespace (foo): {'z': 3}
x: 1, y: 2
~~~
~~~
# Input

x = 1
def foo():
    global x
    x = 11
    print(f"Local Namespace (foo): {locals()}")
foo()
print(f"x: {globals()['x']}")
~~~
~~~
# Output

Local Namespace (foo): {}
x: 11
~~~

---

The variables the follow the nonlocal statement refer to previously bound variables in the nearest enclosing scope other than the global scope.
~~~
# Input

def outer():
    x = 1
    y = 2
    def inner():
        nonlocal x, y
        x = 11
        y = 22
        print(f"Local Namespace (inner): {locals()}")
    inner()
    print(f"Local Namespace (outer): {locals()}")
outer()
~~~
~~~
# Output

Local Namespace (inner): {'y': 22, 'x': 11}
Local Namespace (outer): {'inner': <function outer.<locals>.inner at 0xb787e614>, 'y': 22, 'x': 11}
~~~

---

The variables listed in the nonlocal statement must refer to pre-existing bound variables. Otherwise, an exception is raised.
~~~
# Input

def outer():
    y = 1
    def inner():
        nonlocal x
        x = 11
        print(f"Local Namespace (inner): {locals()}")
    inner()
    print(f"Local Namespace (outer): {locals()}")
outer()
~~~
~~~
# Output
Traceback (most recent call last)
...
SyntaxError: no binding for nonlocal 'x' found
~~~

---

When making an assignment to a variable anywhere within the body of a function, the variable is assumed to be local (it's recognized as local by the compiler) regardless of whether the function is executed or not.
~~~
# Input
x = 1
def foo():
    y = 2
    print(x)
    print(y)
    z = 3
print(foo.__code__.co_varnames)
~~~
~~~
# Output
('y', 'z')
~~~
It's also worth mentioning that making an assignment to a variable in the body of a function only initializes the variable when the function is executed.
~~~
# Input
class Person():
    def __init__(self):
        print("Initialized!")
def foo():
    person = Person()
print("Before execution...")
foo()
print("After execution...")
~~~
~~~
# Output
Before execution...
Initialized!
After execution...
~~~   
With that said, it's simple to see why the following code raises an exception:
~~~
# Input
x = 1
def foo():
    print(x)
    x = 11
foo()
~~~
~~~
# Output
Traceback (most recent call last)
...
UnboundLocalError: local variable 'x' referenced before assignment
~~~
As the last statement in the body of the function assigns a new value to the variable *x*, the variable is treated as local at compile-time. Therefore, passing an uninitialized variable in the *print* function raises an exception.

---

References:

https://www.youtube.com/watch?v=WYZrLtFNDVI

https://docs.python.org/3/tutorial/classes.html#python-scopes-and-namespaces
	
https://docs.python.org/3/faq/programming.html#why-am-i-getting-an-unboundlocalerror-when-the-variable-has-a-value
	
https://docs.python.org/3/reference/simple_stmts.html#global

