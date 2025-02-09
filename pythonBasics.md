# Table of contents
- [Table of contents](#table-of-contents)
- [Comments](#comments)
- [Importing Modules](#importing-modules)
- [Strings](#strings)
- [Advanced strings](#advanced-strings)
- [Math](#math)
- [Variables \& Methods](#variables--methods)
- [Functions](#functions)
- [Boolean Expressions](#boolean-expressions)
- [Relational operators](#relational-operators)
- [Conditional Statements](#conditional-statements)
- [Lists](#lists)
- [Tuples](#tuples)
- [Dictionaries](#dictionaries)
- [Looping](#looping)
- [Sockets](#sockets)

# Comments 
**# this is a comment**

# Importing Modules 
```python
From what import what as alias 

#sys, os, datetime often used 
# Alias if defined instead of writing datetime, you can wtite dt if specified 
```

# Strings

```python
print("string") 
print('string') 
print("""String 
multiple lines""") 
print("string 1 " + "is awesome") 
```

# Advanced strings

```python
[0] #first letter 
[-] #last letter 
.split() #splits words into list 
.join 
# escaping \
.strip() # strip spaces
print("Sentence {}".format(variable)) #concatenating
```

# Math 

1. ***/+-** all supported 
1. ** exponents 
1. **%** modulo 
1. // -dividing without leftovers 

# Variables & Methods 
```python
variable_name = value 
#Method call with dot . Ex. 
value.upper()
 
.upper()
.lower()
.title()
.len(variable) #broj karaktera
.int() #returns integer, does not round!
.float() # returns float
.type()

```

# Functions

```python
#defining functions
def function_name(params): 
    variables with indentation 

# Calling function 
function_name(params) 
```

# Boolean Expressions 

```python
True, False
```

# Relational operators

```python
AND OR
```
# Conditional Statements 

```python
if:
 else: 

if:
 elif:
 else: 
```

# Lists
1.  []
1. Live in brackets 
1. Can be changed

```python
list_name = [list_items, "separated by comma"] 
# [index] - starts from 0 
# [start_index:end_index] 
# [start:] - everything after starting index 
# [:stop] - everything until stop index 
# [-1] - very last item 
.len() 
.append(what) #at end 
.pop(index) #delete last or (index) 
```

# Tuples

1. ()
1. Unchangeable
1. Can just be printed or read

```python
tuple_name = (list_items, 'separated by comma') 
```

# Dictionaries
1.  {}
1. Key, value  
```python
var_name = {key:value, key:value, key: [values, values]} 
employees[key] = [value]  # adding
.update({"key": [values]}) # adding 
.get(key)  # returns value 
```

# Looping

```python

for x in list:
   print(x)

while condition: 
  # what_happens 
  iteraror ++ 
```

# Sockets

1. To connect 2 ports together 
1. Connecting ports and ip addreses 
1. Connect to open port etc. 

```python
s= socket.socket(socket.AD_INET, socket.SOCK_STREAM) 
```








