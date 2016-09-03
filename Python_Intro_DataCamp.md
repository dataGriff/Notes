
## General
* To have same code on same line use ;

## Types
* float
* int
* str
* bool

## Operators
* /+ adds int and concatenates strings
* /* multiplies int and replicates strings
* ** power of
* % modulo

## list
* [a, b, c, d]
* can have lists of lists
* don't forget index starts at 0
* list[1] select by index values
* list[-1] select index from end of values
* list[1:3] selects elements 2 to 3, doesn't return last one
* This behaves the inverse when going from end and using negative numbers
* list[:2] select indexes up to 3rd element as blank is 0 same other way too list [2:]
* Remember lists are held in memory and variables just point at list
* if do x=y then all doing is point x at y as well
* would need to do x=list(y) to make new separate list
* to update listname[1] = value
* to delete del(listname[1])
* to add  listname+list

## Functions
* print()
* type()
* str()
* float()
* int()
* len()
* max()
* round()
* help()
* ?functionname also works
* sorted()

## methods

* everything is an object and they have different available methods
* listname.index("elementname") gets elementname
* listname.count("elementvalue") counts number of elementvalues
* stringname.capitalize()
* stringname.replace()
* stringname.index("a")
* listname.append("elementvalue")
* listname.remove("elementvalue")
* listname.reverse()
* np_array.shape()

## packages
https://pip.pypa.io/en/stable/installing/
```
get-pip.py
python3 get-pip.py
pip3 install numpy
```

* numpy
* matplotlib
* scitkitlearn
* math
* scipy

To import packages
```
import numpy
numpy.array([1,2,3])
import numpy as np # alias
np.array([1,2,3])
from numpy import array # only imports array
array([1,2,3]) # dont know using numpy then though so harder to read
```
You can use math.pi with math package

## numpy

* Numeric python3
* Creates numpy array so can perform calc over arrays
```
pip3 install numpt
```
```
import numpy as np
np.array(list)
```
* Numpy arrays only contain one type
* Therefore coercion takes place when mixed
* It is just another type and contains its own methods
* When you do python lists added together they concatenate but when add numpy lists they calculate the additions
* numpyarrayname[numpyarrayname > value]
* returns those more than value in array

* ndarray = N-dimensional array
* np_2d = ([1,2,3],[4,5,6]) # example
* np_2d[0][2] would return number 3
* You can use semi columns on them to [:][:]
* Basically just lists in lists (rows)
* np_array.shape() says how many rows and columns
* np_array[49,:] # 50th row both cols
* np_array[:,1] # all of second column
* np_array[123,0] # first column of 124 row

* np.mean(np_name[]) # performs a mean
* np.median(np_name[]) # performs a median
* np.corrcoef(np_name[]) # performs a correlaton coefficent
* corr = np.corrcoef(np_baseball[:,0], np_baseball[:,1]) #example
* np.std(np_name[]) # performs a standard deviation
* np.sum(np_name[]) # performs a sum
* other_heights = np_heights[np_positions != 'GK'] # example subset 
