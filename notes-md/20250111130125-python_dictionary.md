
# Table of Contents

1.  [Syntax](#org00fd2fd)
2.  [Characteristics](#orgf64b77f)
3.  [Methods](#orgd2f7bbe)
    1.  [keys()](#orgf2c8216)
        1.  [Use Cases](#org07ceed9)
    2.  [values()](#orgb46283a)
        1.  [Use cases](#orgee51ea1)
    3.  [item()](#org276cf5a)
        1.  [Use Cases](#org0417836)
4.  [See Also](#orgffb44fc)



<a id="org00fd2fd"></a>

# Syntax

A [dictionary](20250111131949-programming_dictionary.md) in Python is simple. You just use the following syntax:

    dictionary = {
        "key1": value,
        "key2": value2,
    }

The keys are strings.

To add a new pair you just do this

    dictionary["key 3"] = 45

This will add the key "key 3" and assign the value 45 in the previous dictionary


<a id="orgf64b77f"></a>

# Characteristics

-   It is a mutable object
-   It doesn't keep the order of the saved pairs <key: value>


<a id="orgd2f7bbe"></a>

# Methods

*Here I will save\\/write the methods that I have use so far*


<a id="orgf2c8216"></a>

## keys()

Return a [list](20250111131854-python_list.md) of the keys in the dictionary


<a id="org07ceed9"></a>

### Use Cases

1.  Verify if exists a key in a dictionary

        dict_example = {
            "key 1": 23,
            "key 2": 32,
            "key 3": 11,
        }
        
        searched_key = "key 4"
        
        if searched_key in dict_example.keys():
            print(f"The key {searched_key} is in the dictionary")
        else:
            print(f"The key {searched_key} is not in the dictionary")
    
    In this example we look for a key and print if it is in the dictionary or not. In this case, the searched key is not in the dictionary

2.  Access every entry in the dictionary

    We can also use this method to acces every value saved in the dictionary
    
        dict_example = {
            "key 1": 23,
            "key 2": 32,
            "key 3": 11,
        }
        
        searched_key = "key 4"
        
        for _ in dict_example.keys():
            print(dict_example[_])
    
    This will print every value saved int the dictionary. In this case the output would be
    
        23
        32
        11


<a id="orgb46283a"></a>

## values()

This method return a list of the values saved in the dictionary. It works similar as the keys method but for the values


<a id="orgee51ea1"></a>

### Use cases

1.  Use the values without modifying and saving them

    We can use this method if we want to use the values but we doesn't need to save the modifications in the dictionary
    
        dict_example = {
            "key 1": 23,
            "key 2": 43,
            "key 3": 54,
        }
        
        for _ in dict_example.values():
            cuadratic = _**2
            print(square)
        
        for _ in dict_example.keys():
            print(dict_example[_])
    
    With this example, we first will see a list of the cuadratics of every number saved in the list and then we'll see that the list didn't change.


<a id="org276cf5a"></a>

## item()

This methos return a list of pairs (key, value) of the dictionary


<a id="org0417836"></a>

### Use Cases

1.  Printing the dictionary

        dict_example = {
            "key 1": 23,
            "key 2": 32,
            "key 3": 11,
        }
        
        for key, value in dict_example.items():
            print(f"{key}: {value}")
    
    The output will be:
    \#+begin<sub>src</sub> bash
    key 1: 23
    key 2: 32
    key 3: 11
    \#+end<sub>src</sub>>


<a id="orgffb44fc"></a>

# See Also

-   [Python List](20250111131854-python_list.md)

