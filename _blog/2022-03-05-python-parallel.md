---
title: Python parallel processing with multiprocessing
tags: python parallel
---


Say we have a function called `write_img(t)` that takes integer values. 
The for loop

```python
for t in range(starting, ending):
	write_img(t)
```

can be replaced by

```python
from multiprocessing import Pool
a_pool = Pool()
a_pool.map(write_img, range(staring, ending))
```

* If the argument of the function is not a number, we can feed an iterator (array, tuple, list, etc) of the input parameters

```python
def myfunc(obj):
	x = obj.x
	y = obj.y
	# some stuff with x and y
	return obj2

from multiprocessing import Pool
input_list = []
for i in range(10):
	obj_i = # some code here ...
	input_list.append(obj_i)

a_pool = Pool()
output_obj2_list = a_pool.map(myfunc, input_list)
```

* If the function takes more than one input, we can use `zip()` to combine input variables or create a partial function to convert it into a one-input function on the fly using `partial` from `functools` (which is included in the default python installation)

```python
def fun2(x, y):
	return z = x * y

from functools import partial
fun1 = fun2(x, 5)

from multiprocessing import Pool
a_pool = Pool()
output_list = a_pool.map(fun1, range(10))
```

* If you get the error 

```
AttributeError: 'NoneType' object has no attribute 'pack'
```

then use

```python
pool.close()
```

after the multiprocessing is over to delete the pool.

* Use `pathos.multiprocessing` (`pip3 install pathos`) instead of usual multiprocessing to use parallel processing on partial functions (to use on functions with multiple inputs)

```python
from pathos.multiprocessing import ProcessingPool as Pool
```
