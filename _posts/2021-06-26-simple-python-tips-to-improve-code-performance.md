---
layout: post
title: Simple Python Tips to Optimize Code Performance
tags: [Python, productivity, code, performance]
thumbnail-img: https://www.anudit.in/assets/img/python_tips/python-tips-logo.png
share-img: https://www.anudit.in/assets/img/python_tips/python-tips-logo.png
---

Python, created by Guido van Rossum and released in 1991, is now an advanced, general-purpose programming language. In contrast with other programming languages such as C++ or JAVA, Python is deemed to be more accessible because of its simplified syntax that stresses code readability. It utilizes substantial whitespace and simplicity as it allows programmers to write models and conceptions in fewer lines of codes.

<center><img src="/assets/img/python_tips/py-joke.jpg" alt="Python Joke"></center>

Improving performances by optimization of code should be a healthy practice employed by every type of coders. Whether you are beginning to write code or already have mastery over the language, it would not harm to look up some ways in which you can improve your code. This practice would also help earn some brownie points in an interview setting.

Python has many business and scientific applications that make it more versatile amongst the other popular programming languages. The most common uses of Python can be seen in Backend Development, Game Development, Data Science and wildly popular Machine Learning. Having a plethora of unique qualities and features makes Python an ideal candidate for coding computer programs. However, there is always room for improvements.

Let's dive into some handy tips to help you get more performance out of your Python code. I have included benchmarks for almost all the tips so that you can observe the improvements in speedups.

<h3>1. Do Not Re-invent the Wheel</h3>

Developers often come across coding time-critical pieces of software where time is money. It would be easy for developers to use built-in functions and libraries that can provide significant speedup instead of writing them again. For instance, the *map()* function can be used if you are planning to write any asynchronous, parallel, or distributed code. Below is a Python program to illustrate library functions:

```python
import timeit

# Using for-loop instead of in-built map.

def without_in_built_map(my_string):

    string_upper = []
    for string_char in my_string:
        string_upper.append(string_char.upper())
    print (string_upper)

# Using in-built map.

def with_in_built_map(my_string):

    string_upper = list(map(str.upper, my_string))
    print (string_upper)

print ('Time taken by without_in_built_map: ',
       timeit.timeit('without_in_built_map("Iron Man")',
       setup='from __main__ import without_in_built_map'))

print ('Time taken by with_in_built_map: ',
       timeit.timeit('with_in_built_map("Iron Man")',
       setup='from __main__ import with_in_built_map'))
```

Let's see these two functions perform with basic benchmarking.

```bash
Time taken by without_in_built_map:  13.761940060999999
Time taken by with_in_built_map:  12.068126550999999
```
<br><br>

<h3>2. Optimize Your Loops</h3>

Loops are an essential part of every software development life cycle. Every developer once in a while has implemented any type of loop while coding. Ever so that there are times when developers need to emphasise the optimisation of loops in their coding solution. While working in Python you can actually use a plethora of techniques for making loops run faster. Let us dive into it and see an illustration for improving for-loop in Python.

*Example 1:*

Let us consider a function that updates the list of Zip Codes. The list strips the trailing spaces with the help of a for-loop:

```python
new_zip_codes = []

for zip_code in old_zip_codes:
    new_zip_codes.append(zip_code.strip())
```

*Example 2:*

To make it more cost-efficient we can convert the above line of codes into a single line using the map object. Something like:

```python
new_zip_codes = map(str.strip, old_zip_codes)
```

*Example 3:*

Another round of optimisation that we can do on this line of code is that we can make it more linear using list comprehensions.

```python
new_zip_codes += [zip.strip() for zip in zip_codes]
```

*Example 4:*

Last and not least, we can make it faster by converting the loop into a generator expression.

```python
itertools.chain(zip_codes, (zip.strip() for zip in new_zip_codes))
```

Now let us club all these examples in a Python code and observe the benchmarks.

```python
import timeit
import itertools

zip_codes = ['121212', '232323', '434334']
new_zip_codes = [
    '131313',
    '242424',
    '212121',
    '323232',
    '342312',
    '565656',
    ]

def update_zips(new_zip_codes, zip_codes):
    for zip_code in new_zip_codes:
        zip_codes.append(zip_code.strip())

def update_zips_with_map(new_zip_codes, zip_codes):
    zip_codes += map(str.strip, new_zip_codes)

def update_zips_with_list_com(new_zip_codes, zip_codes):
    zip_codes += [iter.strip() for iter in new_zip_codes]

def update_zips_with_gen_exp(new_zip_codes, zip_codes):
    return itertools.chain(zip_codes, (iter.strip() for iter in
                           new_zip_codes))

print ('update_zips() Time            : ' \
    + str(timeit.timeit('update_zips(new_zip_codes, zip_codes)',
          setup='from __main__ import update_zips, new_zip_codes, zip_codes'
          )))

zip_codes = ['121212', '232323', '434334']
print ('update_zips_with_map() Time     : ' \
    + str(timeit.timeit('update_zips_with_map(new_zip_codes, zip_codes)'
          ,
          setup='from __main__ import update_zips_with_map, new_zip_codes, zip_codes'
          )))

zip_codes = ['121212', '232323', '434334']
print ('update_zips_with_list_com() Time : ' \
    + str(timeit.timeit('update_zips_with_list_com(new_zip_codes, zip_codes)'
          ,
          setup='from __main__ import update_zips_with_list_com, new_zip_codes, zip_codes'
          )))

zip_codes = ['121212', '232323', '434334']
print ('update_zips_with_gen_exp() Time  : ' \
    + str(timeit.timeit('update_zips_with_gen_exp(new_zip_codes, zip_codes)'
          ,
          setup='from __main__ import update_zips_with_gen_exp, new_zip_codes, zip_codes'
          )))
```

After running the code, we will get the benchmarks something like these:

```python
update_zips() Time            : 1.960164784
update_zips_with_map() Time     : 1.2161386410000001
update_zips_with_list_com() Time : 1.5180594570000001
update_zips_with_gen_exp() Time  : 0.9815816259999997
```
<br><br>

<h3>3. Avoid Using Globals</h3>

Another way in which Python code can be optimized is with minimal usage of global variables. Not only it ensures to generate an effective design pattern but also it helps to keep track of reach, preventing redundant memory usage.

That means using a local variable is recommended as it helps us get more brownie points in terms of execution speed. Python retrieves a local variable way faster than a global one. To help illustrate this, consider the following Python code:

```bash
test_string = "Hello, World!"

def test_func_glob():
    string_arr = []
    for i in range(50):
      string_arr.append(test_string)

def test_func_loc():
    test_string = "Hello, World!"
    string_arr = []
    for i in range(50):
      string_arr.append(test_string)

if __name__ == '__main__':
    import timeit
    print("Time taken by Global : ", timeit.timeit("test_func_glob()", setup="from __main__ import test_func_glob"))
    print("Time taken by Local : ", timeit.timeit("test_func_loc()", setup="from __main__ import test_func_loc"))
```

Observe the time difference in their times when we do a basic benchmark implementation.

```bash
Time taken by Global : 7.0197728790000005
Time taken by Local : 6.58575879
```


<br><br>

<h3>4. Reduce Memory Footprint</h3>

Who does not love that your code is so well optimised that it uses minimal use of resources? Another level of optimisation that you can employ in your code is reducing the memory footprints. But how would you achieve this? Consider the following example:

```python
message_string = 'I\n'
message_string += 'Love\n'
message_string += 'Python\n'
```

These lines of codes seem inefficient because upon each pass new string gets created. Instead, you can use a list and join them together. Here is how:

```python
message_string = ['I', 'Love', 'Python']
'\n'.join(message_string)
```

Similarly, you could eliminate the usage of the + operator on the string.

Consider the following example:

Slower:

```python
message_string = 'Hello ' + my_var + ' World'
```

Better:

```python
message_string = 'Hello {} World'.format(my_var)
```

Faster:

```python
message_string = 'Hello %s World' % my_var
```

Cleaner:

```python
message_string = f'Hello {my_var} World'
```

More like *Harder, Better, Faster, Stronger* by *Daft Punk* but coding style. If you know what I mean.

<br><br>

<h3>5. Use Cache Methods</h3>

As they say, every second count, in programming we are dealing with not only seconds with the tiniest fractions of seconds to improve on performance. Caching is another clever way to make slight improvements in your program. The way Python does this is called the process of Memoization. When a function is being evaluated it simply becomes the matter of looking up the result when we first evaluated it.

Let's consider the following simple class that encloses a list and adds the ability to perform a total summation over it:

```python
class advanced_list:
    def __init__(self, vals_list):
        self.values = vals_list
    def sum(self):
        return sum(self.values)
```

We can then use the following class as follows:

```python
my_list = advanced_list([1] * 10000000) # a list of 10 million ones
my_list.sum() # outputs: 10000000
```

So when each time we call *my_list.sum()*, it will iterate over the list and calculate the summation. This can be very time-consuming and unnecessary if the list remains the same.

Nevertheless, we can come around this by following this code:

```python
class advanced_list:
    def __init__(self, vals_list):
        self.values = vals_list
        self._sum = None
    
    def sum(self):
        if self._sum is None:
            self._sum = sum(self.values)
        
        return self._sum
```

Here we are only calculating the summation once, we store and then we keep returning the stored value immediately.

We can see the difference upon doing some basic benchmarking:

```python
from time import time
my_list = advanced_list([1] * 10000000)

# First time
start = time()
my_list.sum
end = time()
print(f"{(end - start):.5f} second") # 0.03787 second

# Second time
start = time()
my_list.sum
end = time()
print(f"{(end - start):.5f} second") # 0.00004 second
```

<br><br>

<h3>6. Data Aggregation</h3>

Function call overhead in Python is relatively high, in contrast to the execution speed of a built-in function. This implies that wherever applicable, functions should handle data aggregates.

Below is an illustration to help demonstrate this concept.

```python
# Code Version 1

import time
test_number = 0

def doit1(i):
    global test_number
    test_number = test_number + i

list = range(100000)
t = time.time()
for i in list:
    doit1(i)

print ('Time taken by Code 1: %.3f' % (time.time() - t))
```
<br>
```python
# Code Version 2
import time
test_number = 0

def doit2(list):
    global test_number
    for i in list:
        test_number = test_number + i

list = range(100000)
t = time.time()
doit2(list)

print ('Time taken by Code 2: %.3f' % (time.time() - t))
```

The output of these two versions of the code with benchmarking:

```bash
Time taken by Code 1: 0.758
Time taken by Code 2: 0.204
```

You can observe that the second code runs four times more durably than the first.


<br><br>

<h3>7. Avoid Checking if a Variable is True</h3>

A traditional way that coders are used to while looking for an empty variable is to compare them with *None*. While this does make sense, but a little tweak can help you get some bump up in the performance of your application. How would you achieve this? Instead of comparing an object with *None* to check if it is empty or not, you can simply pass it as the only thing in the condition check. 

Here is a small implementation to help you understand this.

```python
import timeit

# Using the Traditional Way

def traditional_way(test_string):

    for letter in test_string:
        if test_string != None:
            print ('Found')
            break
        else:
            print ('Not Found')

# Using the Faster Way

def faster_way(test_string):

    for letter in test_string:
        if test_string:
            print ('Found')
            break
        else:
            print ('Not Found')

print ('Time taken by traditional_way: ',
       timeit.timeit('traditional_way("Hey there! Welcome to Anudit\'s Blog")'
       , setup='from __main__ import traditional_way'))

print ('Time taken by faster_way: ',
       timeit.timeit('faster_way("Hey there! Welcome to Anudit\'s Blog")',
       setup='from __main__ import faster_way'))
```

And here are some basic benchmarks to support this notion.

```bash
Time taken by traditional_way:  5.300449028
Time taken by faster_way:  4.991210322000001
```

<br><br>

<h3>8. Use List Comprehension</h3>

List Comprehension in Python can help you minimise multiple lines of code of the same task in one. It is one of the language's most distinctive features which provides us with a simple way to create a list based on some iterable.

The list comprehensions are more efficient both computationally and in terms of coding space and time than a for-loop. Let us see an example of the speed of a for loop vs the speed of a list comprehension. We will pass the number of executions using the number argument and set this argument to 1 million.

```python
import timeit

# Using For Loop.

def squares(size):
    result = []
    for number in range(size):
        result.append(number * number)
    return result

# Using a List Comprehension

def squares_comprehension(size):
    return [number * number for number in range(size)]

print ('Time taken by For Loop', timeit.timeit('squares(50)',
       'from __main__ import squares', number=1000000))
print ('Time taken by List Comprehension',
       timeit.timeit('squares_comprehension(50)',
       'from __main__ import squares_comprehension', number=1000000))
```

Let us analyze the benchmarks and observe which method was the fastest.

```bash
Time taken by For Loop 7.664531797
Time taken by List Comprehension 4.23257517
```

<br><br>

<h3>9. Avoid using . (dot) operator</h3>

In Python, almost everything is an object which has certain attributes and methods. To connect these two, we typically use a . (dot) operator. But the question is, can we avoid using this dot operator to achieve significant speed bumps? 

Put simply, Yes! we can. Let us see an example where we will avoid using . (dot) operator.

```python
import math
import timeit

def square_root_with_dot(num):
    val = math.sqrt(num)
    return val

print ('Time taken with dot . operator: ',
       timeit.timeit('square_root_with_dot(42)',
       setup='from __main__ import square_root_with_dot'))
```

Instead of using the above approach, you can find the square root something like this:

```python
from math import sqrt
import timeit

def square_root_without_dot(num):
    val = sqrt(42)
    return val

print ('Time taken without dot . operator: ',
       timeit.timeit('square_root_without_dot(42)',
       setup='from __main__ import square_root_without_dot'))
```

The output of these benchmark would look something like:

```bash
Time taken with dot . operator:  0.197880573
Time taken without dot . operator:  0.15837284499999998
```

But how by simply removing a dot it can help us achieve a significant amount of performance? Because when we call a function using . (dot) it first calls *getattribute()* or *getattr()* which then use dictionary operation which costs time. So, we can try using, from module import function.

<br><br>

<h3>10. Use Sets and Unions in place of Nested Loops</h3>

Loops are easy to implement but they put unnecessary strain on your server. Instead, you can use Sets and Unions which are proved to be more efficient than using loops.

Consider an example, here we want to find the overlapping values in two lists. Traditionally, you can use nested for-loops.

```python
import timeit

def overlaps_with_for_loop():
    a = [1,2,3,4,5]
    b = [2,3,4,5,6]

    overlaps = []
    for x in a:
      for y in b:
        if x==y:
          overlaps.append(x)

    return overlaps

print ('Time taken by overlaps_with_for_loop: ',
       timeit.timeit('overlaps_with_for_loop',
       setup='from __main__ import overlaps_with_for_loop'))
```

Now consider this approach:

```python
import timeit

def overlaps_with_set():
    a = [1,2,3,4,5]
    b = [2,3,4,5,6]

    overlaps = set(a) & set(b)

    return overlaps

print ('Time taken by overlaps_with_set: ',
       timeit.timeit('overlaps_with_set',
       setup='from __main__ import overlaps_with_set'))
```

Let us observe the benchmarks obtained after running these aforementioned codes.

```bash
Time taken by overlaps_with_for_loop:  0.042888203999999985
Time taken by overlaps_with_set:  0.019182008
```

I believe these Python performance tips may bring a sea change for you when you want to save significant time and resources. I hope that you would try to incorporate these tips and tricks to make your applications run faster and more efficiently.

Thank you for reading.