# Python Data Structures

Welcome to the **Python Data Structures** repository! This repository is a comprehensive guide to understanding various data structures in Python, complete with definitions, syntax, and examples for each type. Whether you're a beginner or an experienced developer, you'll find valuable information and practical code snippets to enhance your Python programming skills.

## Table of Contents

- [Dictionaries, Maps, and Hash Tables](#dictionaries-maps-and-hash-tables)
  - [dict: Your Go-to Dictionary](#dict-your-go-to-dictionary)
  - [collections.OrderedDict: Remember the Insertion Order of Keys](#collectionsordereddict-remember-the-insertion-order-of-keys)
  - [collections.defaultdict: Return Default Values for Missing Keys](#collectionsdefaultdict-return-default-values-for-missing-keys)
  - [collections.ChainMap: Search Multiple Dictionaries as a Single Mapping](#collectionschainmap-search-multiple-dictionaries-as-a-single-mapping)
  - [types.MappingProxyType: A Wrapper for Making Read-Only Dictionaries](#typesmappingproxytype-a-wrapper-for-making-read-only-dictionaries)
- [Array Data Structures](#array-data-structures)
  - [list: Mutable Dynamic Arrays](#list-mutable-dynamic-arrays)
  - [tuple: Immutable Containers](#tuple-immutable-containers)
  - [array.array: Basic Typed Arrays](#arrayarray-basic-typed-arrays)
  - [str: Immutable Arrays of Unicode Characters](#str-immutable-arrays-of-unicode-characters)
  - [bytes: Immutable Arrays of Single Bytes](#bytes-immutable-arrays-of-single-bytes)
  - [bytearray: Mutable Arrays of Single Bytes](#bytearray-mutable-arrays-of-single-bytes)
- [Records, Structs, and Data Transfer Objects](#records-structs-and-data-transfer-objects)
  - [dict: Simple Data Objects](#dict-simple-data-objects)
  - [tuple: Immutable Groups of Objects](#tuple-immutable-groups-of-objects)
  - [Write a Custom Class: More Work, More Control](#write-a-custom-class-more-work-more-control)
  - [dataclasses.dataclass: Python 3.7+ Data Classes](#dataclassesdataclass-python-37-data-classes)
  - [collections.namedtuple: Convenient Data Objects](#collectionsnamedtuple-convenient-data-objects)
  - [typing.NamedTuple: Improved Namedtuples](#typingnamedtuple-improved-namedtuples)
  - [struct.Struct: Serialized C Structs](#structstruct-serialized-c-structs)
  - [types.SimpleNamespace: Fancy Attribute Access](#typessimplenamespace-fancy-attribute-access)
- [Sets and Multisets](#sets-and-multisets)
  - [set: Your Go-to Set](#set-your-go-to-set)
  - [frozenset: Immutable Sets](#frozenset-immutable-sets)
  - [collections.Counter: Multisets](#collectionscounter-multisets)
- [Stacks (LIFOs)](#stacks-lifos)
  - [list: Simple, Built-in Stacks](#list-simple-built-in-stacks)
  - [collections.deque: Fast and Robust Stacks](#collectionsdeque-fast-and-robust-stacks)
  - [queue.LifoQueue: Locking Semantics for Parallel Computing](#queuelifoqueue-locking-semantics-for-parallel-computing)
- [Queues (FIFOs)](#queues-fifos)
  - [list: Terribly Sloooow Queues](#list-terribly-sloooow-queues)
  - [collections.deque: Fast and Robust Queues](#collectionsdeque-fast-and-robust-queues)
  - [queue.Queue: Locking Semantics for Parallel Computing](#queuequeue-locking-semantics-for-parallel-computing)
  - [multiprocessing.Queue: Shared Job Queues](#multiprocessingqueue-shared-job-queues)
- [Priority Queues](#priority-queues)
  - [list: Manually Sorted Queues](#list-manually-sorted-queues)
  - [heapq: List-Based Binary Heaps](#heapq-list-based-binary-heaps)
  - [queue.PriorityQueue: Beautiful Priority Queues](#queuepriorityqueue-beautiful-priority-queues)
- [Conclusion: Python Data Structures](#conclusion-python-data-structures)

## Dictionaries, Maps, and Hash Tables

### dict: Your Go-to Dictionary
A dictionary in Python is a collection of key-value pairs. It is mutable, and the keys must be unique and immutable.

**Syntax**:
```python
my_dict = {
    "key1": "value1",
    "key2": "value2"
}
```

**Example**:
```python
# Creating a dictionary
my_dict = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

# Accessing values
print(my_dict["name"])  # Output: Alice

# Adding a new key-value pair
my_dict["email"] = "alice@example.com"

# Updating a value
my_dict["age"] = 31

# Deleting a key-value pair
del my_dict["city"]

print(my_dict)
```

### collections.OrderedDict: Remember the Insertion Order of Keys
`OrderedDict` is a dictionary subclass in the `collections` module that remembers the order in which keys were first inserted.

**Syntax**:
```python
from collections import OrderedDict

ordered_dict = OrderedDict()
ordered_dict[key] = value
```

**Example**:
```python
from collections import OrderedDict

# Creating an OrderedDict
ordered_dict = OrderedDict()
ordered_dict["name"] = "Alice"
ordered_dict["age"] = 30
ordered_dict["city"] = "New York"

print(ordered_dict)  # Output: OrderedDict([('name', 'Alice'), ('age', 30), ('city', 'New York')])
```

### collections.defaultdict: Return Default Values for Missing Keys
`defaultdict` is a subclass of the built-in `dict` class. It provides a default value for the key that does not exist.

**Syntax**:
```python
from collections import defaultdict

default_dict = defaultdict(default_factory)
```

**Example**:
```python
from collections import defaultdict

# Using int as the default_factory, which provides a default value of 0
default_dict = defaultdict(int)
default_dict["count"] += 1

# Using list as the default_factory, which provides a default value of an empty list
default_list_dict = defaultdict(list)
default_list_dict["fruits"].append("apple")

print(default_dict)        # Output: defaultdict(<class 'int'>, {'count': 1})
print(default_list_dict)   # Output: defaultdict(<class 'list'>, {'fruits': ['apple']})
```

### collections.ChainMap: Search Multiple Dictionaries as a Single Mapping
`ChainMap` groups multiple dictionaries or other mappings together to create a single, updateable view.

**Syntax**:
```python
from collections import ChainMap

chain = ChainMap(dict1, dict2, ...)
```

**Example**:
```python
from collections import ChainMap

# Creating two dictionaries
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

# Combining them into a ChainMap
chain = ChainMap(dict1, dict2)

print(chain["a"])  # Output: 1 (from dict1)
print(chain["b"])  # Output: 2 (from dict1, as it appears first)
print(chain["c"])  # Output: 4 (from dict2)
```

### types.MappingProxyType: A Wrapper for Making Read-Only Dictionaries
`MappingProxyType` is a wrapper around a standard dictionary that provides a read-only view of the dictionary.

**Syntax**:
```python
from types import MappingProxyType

read_only_dict = MappingProxyType(original_dict)
```

**Example**:
```python
from types import MappingProxyType

# Creating a dictionary
original_dict = {"name": "Alice", "age": 30}

# Creating a read-only view
read_only_dict = MappingProxyType(original_dict)

print(read_only_dict["name"])  # Output: Alice

# Attempting to modify will raise a TypeError
# read_only_dict["age"] = 31  # Uncommenting this line will raise an error

# The original dictionary can still be modified
original_dict["age"] = 31
print(read_only_dict["age"])  # Output: 31
```

## Array Data Structures

### list: Mutable Dynamic Arrays
A list is a collection which is ordered and changeable. Allows duplicate members.

**Syntax**:
```python
my_list = [element1, element2, element3]
```

**Example**:
```python
# Creating a list
my_list = [1, 2, 3, 4, 5]

# Accessing elements
print(my_list[0])  # Output: 1

# Modifying elements
my_list[1] = 10

# Adding elements
my_list.append(6)

# Removing elements
my_list.remove(3)

print(my_list)  # Output: [1, 10, 4, 5, 6]
```

### tuple: Immutable Containers
A tuple is a collection which is ordered and unchangeable. Allows duplicate members.

**Syntax**:
```python
my_tuple = (element1, element2, element3)
```

**Example**:
```python
#

 Creating a tuple
my_tuple = (1, 2, 3, 4, 5)

# Accessing elements
print(my_tuple[0])  # Output: 1

# Tuples are immutable, so we cannot change their values
# my_tuple[1] = 10  # This will raise an error

# Tuple concatenation
new_tuple = my_tuple + (6, 7, 8)

print(new_tuple)  # Output: (1, 2, 3, 4, 5, 6, 7, 8)
```

### array.array: Basic Typed Arrays
`array.array` provides a compact and efficient way to store basic types such as integers and floating-point numbers.

**Syntax**:
```python
import array

my_array = array.array(typecode, [initializer_list])
```

**Example**:
```python
import array

# Creating an array of integers
my_array = array.array('i', [1, 2, 3, 4, 5])

# Accessing elements
print(my_array[0])  # Output: 1

# Modifying elements
my_array[1] = 10

# Adding elements
my_array.append(6)

# Removing elements
my_array.remove(3)

print(my_array)  # Output: array('i', [1, 10, 4, 5, 6])
```

### str: Immutable Arrays of Unicode Characters
A string in Python is a sequence of Unicode characters. Strings are immutable.

**Syntax**:
```python
my_str = "Hello, World!"
```

**Example**:
```python
# Creating a string
my_str = "Hello, World!"

# Accessing characters
print(my_str[0])  # Output: H

# Strings are immutable, so we cannot change their values
# my_str[1] = 'a'  # This will raise an error

# String concatenation
new_str = my_str + " How are you?"

print(new_str)  # Output: Hello, World! How are you?
```

### bytes: Immutable Arrays of Single Bytes
A `bytes` object is an immutable sequence of single bytes.

**Syntax**:
```python
my_bytes = b"Hello, World!"
```

**Example**:
```python
# Creating a bytes object
my_bytes = b"Hello, World!"

# Accessing bytes
print(my_bytes[0])  # Output: 72 (ASCII value of 'H')

# Bytes are immutable, so we cannot change their values
# my_bytes[1] = 97  # This will raise an error

# Bytes concatenation
new_bytes = my_bytes + b" How are you?"

print(new_bytes)  # Output: b'Hello, World! How are you?'
```

### bytearray: Mutable Arrays of Single Bytes
A `bytearray` object is a mutable sequence of single bytes.

**Syntax**:
```python
my_bytearray = bytearray(b"Hello, World!")
```

**Example**:
```python
# Creating a bytearray object
my_bytearray = bytearray(b"Hello, World!")

# Accessing bytes
print(my_bytearray[0])  # Output: 72 (ASCII value of 'H')

# Modifying bytes
my_bytearray[1] = 97

# Adding bytes
my_bytearray.extend(b" How are you?")

# Removing bytes
del my_bytearray[5:12]

print(my_bytearray)  # Output: bytearray(b'Hallo! How are you?')
```

## Records, Structs, and Data Transfer Objects

### dict: Simple Data Objects
A dictionary can be used to store simple data objects.

**Syntax**:
```python
data_object = {
    "field1": value1,
    "field2": value2
}
```

**Example**:
```python
# Creating a data object using a dictionary
data_object = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

# Accessing fields
print(data_object["name"])  # Output: Alice

# Modifying fields
data_object["age"] = 31

print(data_object)
```

### tuple: Immutable Groups of Objects
A tuple can be used to store groups of objects. It is immutable.

**Syntax**:
```python
data_object = (value1, value2, value3)
```

**Example**:
```python
# Creating a data object using a tuple
data_object = ("Alice", 30, "New York")

# Accessing fields
print(data_object[0])  # Output: Alice

# Tuples are immutable, so we cannot change their values
# data_object[1] = 31  # This will raise an error

print(data_object)
```

### Write a Custom Class: More Work, More Control
Custom classes provide more control and flexibility for creating complex data objects.

**Syntax**:
```python
class MyDataObject:
    def __init__(self, field1, field2):
        self.field1 = field1
        self.field2 = field2
```

**Example**:
```python
# Creating a custom class
class Person:
    def __init__(self, name, age, city):
        self.name = name
        self.age = age
        self.city = city

# Creating an instance of the custom class
person = Person("Alice", 30, "New York")

# Accessing fields
print(person.name)  # Output: Alice

# Modifying fields
person.age = 31

print(person)
```

### dataclasses.dataclass: Python 3.7+ Data Classes
`dataclass` provides a decorator and functions for automatically adding special methods to user-defined classes.

**Syntax**:
```python
from dataclasses import dataclass

@dataclass
class MyDataObject:
    field1: type
    field2: type
```

**Example**:
```python
from dataclasses import dataclass

# Creating a data class
@dataclass
class Person:
    name: str
    age: int
    city: str

# Creating an instance of the data class
person = Person("Alice", 30, "New York")

# Accessing fields
print(person.name)  # Output: Alice

# Modifying fields
person.age = 31

print(person)
```

### collections.namedtuple: Convenient Data Objects
`namedtuple` is a factory function for creating tuple subclasses with named fields.

**Syntax**:
```python
from collections import namedtuple

MyDataObject = namedtuple("MyDataObject", ["field1", "field2"])
```

**Example**:
```python
from collections import namedtuple

# Creating a named tuple
Person = namedtuple("Person", ["name", "age", "city"])

# Creating an instance of the named tuple
person = Person("Alice", 30, "New York")

# Accessing fields
print(person.name)  # Output: Alice

# Named tuples are immutable, so we cannot change their values
# person.age = 31  # This will raise an error

print(person)
```

### typing.NamedTuple: Improved Namedtuples
`NamedTuple` provides an improved way of defining named tuples with type annotations.

**Syntax**:
```python
from typing import NamedTuple

class MyDataObject(NamedTuple):
    field1: type
    field2: type
```

**Example**:
```python
from typing import NamedTuple

# Creating an improved named tuple
class Person(NamedTuple):
    name: str
    age: int
    city: str

# Creating an instance of the improved named tuple
person = Person("Alice", 30, "New York")

# Accessing fields
print(person.name)  # Output: Alice

# Named tuples are immutable, so we cannot change their values
# person.age = 31  # This will raise an error

print(person)
```

### struct.Struct: Serialized C Structs
`struct` provides functions to work with C-style data structures in Python.

**Syntax**:
```python
import struct

packed_data = struct.pack(format, value1, value2)
```

**Example**:
```python
import struct

# Packing data into a C-style struct
packed_data = struct.pack('i4s', 7, b'test')

# Unpacking data from a C-style struct
unpacked_data = struct.unpack('i4s', packed_data)

print(unpacked_data)  # Output: (7, b'test')
```

### types.SimpleNamespace: Fancy Attribute Access
`SimpleNamespace` provides simple attribute access for dynamic attribute management.

**Syntax**:
```python
from types import SimpleNamespace

data_object = SimpleNamespace(field1=value1, field2=value2)
```

**Example**:
```python
from types import SimpleNamespace

# Creating a SimpleNamespace object
person = SimpleNamespace(name="Alice", age=30, city="New York")

# Accessing fields
print(person.name)  # Output: Alice

# Modifying fields
person.age = 31

print(person)
```

## Sets and Multisets

### set: Your Go-to Set
A set is an unordered collection with no duplicate elements.

**Syntax**:
```python
my_set = {element1, element2, element3}
```

**Example**:
```python
# Creating a set
my_set = {1, 2, 3, 4, 5}

# Adding elements
my_set.add(6)

# Removing elements
my_set.remove(3)

# Checking membership
print(4 in my_set)  # Output:

 True

print(my_set)  # Output: {1, 2, 4, 5, 6}
```

### frozenset: Immutable Sets
A `frozenset` is an immutable version of a set.

**Syntax**:
```python
my_frozenset = frozenset([element1, element2, element3])
```

**Example**:
```python
# Creating a frozenset
my_frozenset = frozenset([1, 2, 3, 4, 5])

# Frozensets are immutable, so we cannot modify them
# my_frozenset.add(6)  # This will raise an error

print(my_frozenset)  # Output: frozenset({1, 2, 3, 4, 5})
```

### collections.Counter: Multisets
`Counter` is a subclass of `dict` for counting hashable objects.

**Syntax**:
```python
from collections import Counter

counter = Counter(iterable)
```

**Example**:
```python
from collections import Counter

# Creating a Counter object
counter = Counter([1, 2, 2, 3, 3, 3, 4, 4, 4, 4])

# Accessing counts
print(counter[2])  # Output: 2

# Updating counts
counter.update([2, 3, 3])

print(counter)  # Output: Counter({4: 4, 3: 5, 2: 3, 1: 1})
```

## Stacks (LIFOs)

### list: Simple, Built-in Stacks
A list can be used as a simple stack (Last In, First Out).

**Syntax**:
```python
stack = []
stack.append(element)  # Push
stack.pop()            # Pop
```

**Example**:
```python
# Creating a stack
stack = []

# Pushing elements
stack.append(1)
stack.append(2)
stack.append(3)

# Popping elements
print(stack.pop())  # Output: 3
print(stack.pop())  # Output: 2

print(stack)  # Output: [1]
```

### collections.deque: Fast and Robust Stacks
`deque` provides a double-ended queue which can be used as a stack.

**Syntax**:
```python
from collections import deque

stack = deque()
stack.append(element)  # Push
stack.pop()            # Pop
```

**Example**:
```python
from collections import deque

# Creating a deque stack
stack = deque()

# Pushing elements
stack.append(1)
stack.append(2)
stack.append(3)

# Popping elements
print(stack.pop())  # Output: 3
print(stack.pop())  # Output: 2

print(stack)  # Output: deque([1])
```

### queue.LifoQueue: Locking Semantics for Parallel Computing
`LifoQueue` provides a thread-safe stack implementation.

**Syntax**:
```python
from queue import LifoQueue

stack = LifoQueue()
stack.put(element)  # Push
stack.get()         # Pop
```

**Example**:
```python
from queue import LifoQueue

# Creating a LifoQueue stack
stack = LifoQueue()

# Pushing elements
stack.put(1)
stack.put(2)
stack.put(3)

# Popping elements
print(stack.get())  # Output: 3
print(stack.get())  # Output: 2

print(stack.qsize())  # Output: 1
```

## Queues (FIFOs)

### list: Terribly Sloooow Queues
A list can be used as a queue (First In, First Out), but it's inefficient.

**Syntax**:
```python
queue = []
queue.append(element)  # Enqueue
queue.pop(0)           # Dequeue
```

**Example**:
```python
# Creating a queue
queue = []

# Enqueuing elements
queue.append(1)
queue.append(2)
queue.append(3)

# Dequeuing elements
print(queue.pop(0))  # Output: 1
print(queue.pop(0))  # Output: 2

print(queue)  # Output: [3]
```

### collections.deque: Fast and Robust Queues
`deque` provides a double-ended queue which can be used as a queue.

**Syntax**:
```python
from collections import deque

queue = deque()
queue.append(element)  # Enqueue
queue.popleft()        # Dequeue
```

**Example**:
```python
from collections import deque

# Creating a deque queue
queue = deque()

# Enqueuing elements
queue.append(1)
queue.append(2)
queue.append(3)

# Dequeuing elements
print(queue.popleft())  # Output: 1
print(queue.popleft())  # Output: 2

print(queue)  # Output: deque([3])
```

### queue.Queue: Locking Semantics for Parallel Computing
`Queue` provides a thread-safe queue implementation.

**Syntax**:
```python
from queue import Queue

queue = Queue()
queue.put(element)  # Enqueue
queue.get()         # Dequeue
```

**Example**:
```python
from queue import Queue

# Creating a Queue
queue = Queue()

# Enqueuing elements
queue.put(1)
queue.put(2)
queue.put(3)

# Dequeuing elements
print(queue.get())  # Output: 1
print(queue.get())  # Output: 2

print(queue.qsize())  # Output: 1
```

### multiprocessing.Queue: Shared Job Queues
`multiprocessing.Queue` provides shared job queues for multiprocessing.

**Syntax**:
```python
from multiprocessing import Queue

queue = Queue()
queue.put(element)  # Enqueue
queue.get()         # Dequeue
```

**Example**:
```python
from multiprocessing import Queue

# Creating a multiprocessing Queue
queue = Queue()

# Enqueuing elements
queue.put(1)
queue.put(2)
queue.put(3)

# Dequeuing elements
print(queue.get())  # Output: 1
print(queue.get())  # Output: 2

print(queue.qsize())  # Output: 1
```

## Priority Queues

### list: Manually Sorted Queues
A list can be used as a manually sorted priority queue.

**Syntax**:
```python
priority_queue = []
priority_queue.append((priority, element))
priority_queue.sort()
priority_queue.pop(0)  # Dequeue
```

**Example**:
```python
# Creating a priority queue
priority_queue = []

# Enqueuing elements with priorities
priority_queue.append((2, "low priority"))
priority_queue.append((1, "high priority"))
priority_queue.append((3, "medium priority"))

# Sorting the queue
priority_queue.sort()

# Dequeuing elements
print(priority_queue.pop(0))  # Output: (1, 'high priority')
print(priority_queue.pop(0))  # Output: (2, 'low priority')

print(priority_queue)  # Output: [(3, 'medium priority')]
```

### heapq: List-Based Binary Heaps
`heapq` provides an implementation of the heap queue algorithm, also known as the priority queue algorithm.

**Syntax**:
```python
import heapq

heap = []
heapq.heappush(heap, element)
heapq.heappop(heap)
```

**Example**:
```python
import heapq

# Creating a heap
heap = []

# Enqueuing elements
heapq.heappush(heap, (2, "low priority"))
heapq.heappush(heap, (1, "high priority"))
heapq.heappush(heap, (3, "medium priority"))

# Dequeuing elements
print(heapq.heappop(heap))  # Output: (1, 'high priority')
print(heapq.heappop(heap))  # Output: (2, 'low priority')

print(heap)  # Output: [(3, 'medium priority')]
```

### queue.PriorityQueue: Beautiful Priority Queues
`PriorityQueue` provides a thread-safe priority queue implementation.

**Syntax**:
```python
from queue import PriorityQueue

priority_queue = PriorityQueue()
priority_queue.put((priority, element))  # Enqueue
priority_queue.get()                     # Dequeue
```

**Example**:
```python
from queue import PriorityQueue

# Creating a PriorityQueue
priority_queue = PriorityQueue()

# Enqueuing elements with priorities
priority_queue.put((2, "low priority"))
priority_queue.put((1, "high priority"))
priority_queue.put((3, "medium priority"))

# Dequeuing elements
print(priority_queue.get())  # Output: (1, 'high priority')
print(priority_queue.get())  # Output: (2, 'low priority')

print(priority_queue.qsize())  # Output: 1
```

.

