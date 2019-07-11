# 2. Data Structures 

## Lesson 5: Maps and Hashing 

___

### 1. Introduction to Maps 

The defining characteristic of a map is its *key value structure*.

You can look up where something is by its key value and then get whatever is stored at that value. 

We can look up something by its name and then go that that location to get the value. 

Maps are also called dictionaries. 

If you think of a word as a key and the definition as the value. 

___

### 2. Sets and Maps

A set is comparable to a list, its also vaguely a collection of things, but with one big difference.

A list has some kind of ordering for its elements. While a set doesn't have that, but instead doesn't allow for repeated elements. 

You can think of a set kind of like a bag. You can reach in and pull something out, but you will never know what order you're getting the elements out in. 

                              Map = < Key, Value >

A map is a set-based data structure, kind of like an array is a list-based data structure. 

A group of keys is a set. 

The keys in the map, like a dictionary, need to be unique. 

You can have several definitions for the same word stored in the value, but if you had the same word in the dictionary many times, you would randomly pick out a definition when you were first looking. 

Thus, each key exists once in a Map. 

A groupd ot this unique keys without any ordering is called a set. 


___

### 3. Exploring the Map Concept 

In Python, the map concept appears as a built-in data type called a dictionary. A dictionary contains key-value pairs. Dictionaries might soon become your favorite data structure in Python—they're extremely easy to use and useful. Here's a sample of setting up a dictionary. 

```Python
udacity = {}
udacity['u'] = 1
udacity['d'] = 2
udacity['a'] = 3
udacity['c'] = 4
udacity['i'] = 5
udacity['t'] = 6
udacity['y'] = 7

print (udacity)
# {'u': 1, 'd': 2, 'a': 3, 'c': 4, 'i': 5, 't': 6, 'y': 7}
```
In this case, the letters in "udacity" were each keys in our dictionary, and the position of that letter in the string was the value. Thus, I can do the following:

```Python
print (udacity['t'])
# 6
```

This statement is saying "go to the key labeled 't' and find it's value, 6".

Dictionaries are wonderfully flexible—you can store a wide variety of structures as values. You store another dictionary or a list:

```Python
dictionary = {}
dictionary['d'] = [1]
dictionary['i'] = [2]
dictionary['c'] = [3]
dictionary['t'] = [4]
dictionary['i'].append(5)
dictionary['o'] = [6]
dictionary['n'] = [7]
dictionary['a'] = [8]
dictionary['r'] = [9]
dictionary['y'] = [10]
print (dictionary)
# {'d': [1], 'i': [2, 5], 'c': [3], 't': [4], 'o': [6], 'n': [7], 'a': [8], 'r': [9], 'y':[10]}
```

```Python
Time to play with Python dictionaries! You're going to work on a dictionary that stores cities by country and continent. One is done for you - the city of Mountain View is in the USA, which is in North America.

You need to add the cities listed below by modifying the structure. Then, you should print out the values specified by looking them up in the structure.

Cities to add: Bangalore (India, Asia) Atlanta (USA, North America) Cairo (Egypt, Africa) Shanghai (China, Asia)

locations = {'North America': {'USA': ['Mountain View']}}

Print the following (using "print").

A list of all cities in the USA in alphabetic order.
All cities in Asia, in alphabetic order, next to the name of the country. In your output, label each answer with a number so it looks like this:
1
American City
American City
2
Asian City - Country
Asian City - Country

```
```Python
# Code

locations = {'North America': {'USA': ['Mountain View']}}

# TODO: Print a list of all cities in the USA in alphabetic order.

# TODO: Print all cities in Asia, in alphabetic order, next to the name of the country

```

____

<details><summary><b>Solution</b></summary>
<p>

```Python 
locations = {'North America': {'USA': ['Mountain View']}}
locations['North America']['USA'].append('Atlanta')
locations['Asia'] = {'India': ['Bangalore']}
locations['Asia']['China'] = ['Shanghai']
locations['Africa'] = {'Egypt': ['Cairo']}

usa_sorted = sorted(locations['North America']['USA'])
print (1)
for city in usa_sorted:
    print (city)

asia_cities = []
print (2)
for countries, cities in locations['Asia'].items():
    city_country = cities[0] + " - " + countries 
    asia_cities.append(city_country)
asia_sorted = sorted(asia_cities)
for city in asia_sorted:
    print (city)

```
</p>
</details>

___


### 4. Introduction to Hashing

Using a data structure that employs a hash function allow you to do look ups in *constant time*.

With everything we learned so far, we do looks ups in *linear time* 

In a list or a set, you need to look through every element to find the one you're looking for. 

Stacks and Queues let you look up the oldest or newest elements immediately, and priority queues will let you find the highest priority elements quickly. 

The ability to do *constant time* look ups will make almost any algorithm you write instantly faster. 

___

### 5. Hashing

The purpose of a hash function is transform some value into one that can be stored and retrieved easily. 

You give it some value, it converts the value based on some formula, and spits out a coded version of the value that's often the index in an array.  

One common pattern in hash functions is to take the last few digits of a big number, divide it by some consistent number, and using the remainder from that division to find a place to store that number in a array. 

Example:

0123456 --> 56/10 = 5 with a remainder = 6 

6 | 0123456 

Give your number to a hash function, which spits out a hash code that turns into the index of an array. You can go to your array and get your orginial value in constant time. Since the array look up with an index happens in constant time. 


___

### 6. Collisions 

There are times when a hash function will spit out the same value for two different inputs. 

0123456 --> 56% of 10 = 6 

6543216 --> 16% of 10 = 6

This situation is called a **collision**.

There are two main ways to fix a collision. 

The first is to change the value in your hash function, or to change the hash function completely, so you have more than enough slots to store all of your potential values. 

Or instead of storing one hash value in each spot, you could store some type of list that contains all values hashed at that spot. These lists are generally called **buckets**. 

Buckets contain a collection of values.

You can maintain constant time look up, but by using a bigger number in your hash function, you're going to require a lot more space to store your values. Also if you do this reactively and change the value in your hash function every time you have a collision, moving all your data to a new array is going to definitely increase the complexity in terms of both size and time. 

With the bucket approach, you still need to iterate through some collection, though a shorter one, every time you're looking for something. 

Collisions in worst case complexity is **O(m)**.

You are expected to talk about the upsides and downsides to which every approach you use. 

___

### 7. Hash Maps

You can use the keys as inputs to a hash function, then store the key value pair in the bucket of the hash value producded by the function. 

Since you know that the keys in a map are unique since they belong to a set. You could use a hash function to give them each their own unique buckets. 

You could also design a hash function to allow for collisions. 

___

### 8. Hash Maps Notebook 
