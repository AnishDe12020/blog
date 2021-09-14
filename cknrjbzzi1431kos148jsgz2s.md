## The Random Library in Python

You might need your program to choose a random lucky winner from a list of people participating in a lottery or maybe you want to chooses a random fruit from a list of fruits the doctor made you. There are many use cases for this library and let us see how we can use this library.

# Installation and Importing

The library is included with the normal python installation so you don't need to install using `pip`

We need to import the library though so let us do that real quick
```python
import random
```
# Important and Common functions
## `random.choice()`

Now that we have imported the library, let us quickly go through some of the common and important functions the library comes with

Let us see `random.choice()` first
This will pick a random item from any iterable object (list, string etc.)

Example:
```python
import random

list = ["banana", "apple", "guava", "cherry", "strawberry", "mango"]
print(random.choice(list))
# Will pick any random fruit from the list and print that

str = "Coronavirus cases have spiked again!!!"
print(random.choice(str))
# Will pick any random character from the string and print it out
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619011131901/tCxW4n6sG.png)
So in the above image we can see that each and every time the function is run, it will print out a different value as it is picking out randomly

## `random.randrange()`

Now this is an interesting function and probably the one most are looking for. It basically picks out a random number from a range of numbers

Example:
```python
import random

print(random.randrange(1, 20, 2))
# Now it will print out any random number amongst 1, 3, 5, 7, 9, 11, 13, 15, 17 and 19
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619012224758/YGFpml6fm.png)

There are 3 arguments taken in of which the first two are compulsory and third one is optional and be default `1`. But what are the arguments?

1. The first argument is the number from which the range starts
2. The second argument is the number where the range ends
3. The third argument is the step which is the number of numbers to skip while making the list of the numbers

Now does that sound similar?
Yes, this are the exact same arguments take in by the `range` function which is in-built in Python. The `random.randrange()` function basically creates a list from the range with the arguments given and then picks out a random.

## `random.random()`
Now this one is a pretty simple one. It returns a float value between 0 and 1

Example:
```python
import random

print(random.random())
```


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619012345562/7hvScY8I0.png)

## `random.seed()`
Now this one is a bit tough to understand. So the seed function is basically used to save the state of a random function so that it can generate some random numbers on multiple executions of the code on the same machine or on a different machine for a specific seed value. The seed value is the previous random value generated by the generator or if run for the first time, it is set to the current system time.

Example:
```python
import random

random.seed(10)
print("A mapped random number with seed 10 is: " + random.random())
```


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619012999682/zBSuSyECY.png)

## `random.shuffle()`
As the name of the function suggests, we can use it to shuffle a list i.e. change the position of the items in the list.

Example:
```python
import random

cities = ["London", "Bangalore", "Delhi", "Mumbai", "Tokyo", "New York City"]

print("List before shuffling: ")
print(cities)
print("List after shuffling: ")
random.shuffle(cities)
print(cities)
```


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619013686663/udyuXWOr0.png)

## `random.uniform()`
This one is pretty similar to `random.randrange()` but then returns a `float` value instead of an `integer` value and does not take any step in input

Arguments:
1. Lower Limit - included in generation
2. Upper Limit - Excluded in generation

Example:
```python
import random

print(random.uniform(10, 15))
```


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619013874416/Up-dkAYDWMn.png)

## `random.randint()`
Takes 2 arguments as the lower limit and the upper limit. The returned number is between these 2 values and can be anyone of them as well.

Example:
```python
import random

random.randint(50, 100)
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619069311578/TV5dVrBER.png)

So that was some of the most important and commonly used functions of the `random` package and that is it for this blog!!!

[Link](https://docs.python.org/3/library/random.html) to random package docs if you want to explore more - https://docs.python.org/3/library/random.html