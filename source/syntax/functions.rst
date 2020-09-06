Functions
---------

General Functions Syntax
~~~~~~~~~~~~~~~~~~~~~~~~

Functions of the defined syntax have a really simple and generic style:

::

    - result_item = item.function(arg1, arg2, ...)

It's not possible to define new function types within the script. Only a preset can be used. This way the complexity should stay as simple as possible. 

Basically the function call on an item generates a new value, which has its scope where the item and the function call was located. This change is only limited to this location. All other locations where the same item is used are unaffected by the function call. 

In the simplest version, the function has no arguments like this:

::

    - result_item = item.function()

The function can also have one or more arguments. These can be either hard coded values or items themselves:

::

    - result_item = item1.function("test-string", 42)
    - result_item = item1.function(item2)

After a function was called on a item, the result of the call is written back as temporary value itself. So it's possible to call another function to modify the result of the first function call:

::

    - result_item = item.function1().function2()

And because an argument can be a item too, this argument item can also have its own function call like this:

::

    - result_item = item1.function1(item2.function2(item3))



**Restrictions**

    * something like:

      ::

          - input = "test-string".size()

      doesn't work, because it always has to be an item. Instead of this it has to be like this

      ::

          - test_value = "test-string"

          ...

          - input = test_value.size()



.. raw:: latex

    \newpage
    

Function Types
~~~~~~~~~~~~~~

The following are the current presets of available function types.


``size``
^^^^^^^^

Get the size of an item.


**Example**:

::

    - packages = [ "nano", "vim" ]

    if(packages.size() == 2)
    {
        ...
    }

**Arguments**:

    no arguments

**Output Type**:

    int-value

**Input Item**:

.. tabularcolumns:: |m{0.27\textwidth}|m{0.66\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Item type**
      - **Output Content**

    * - map-item
      - number of key-value pairs in the map

    * - array-item
      - number of elements in the array
     
    * - string-value
      - length of the string
     
    * - int-value
      - 0

    * - float-value
      - 0
     
    * - bool-value
      - 0


``append``
^^^^^^^^^^

Add a new item to an existing list.


**Example**:

::

    - packages = [ "nano", "vim" ]

    if(packages.append("gedit").size() == 3)
    {
        ...
    }

**Arguments**:

.. tabularcolumns:: |m{0.1\textwidth}|m{0.2\textwidth}|m{0.63\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Position**
      - **Type**
      - **Content**

    * - 1
      - any data-item
      - new object, which should be added to the existing array

**Output Type**:

    array-item

**Input Item**:

.. tabularcolumns:: |m{0.29\textwidth}|m{0.23\textwidth}|m{0.40\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Item Type**
      - **Argument**
      - **Output Content**

    * - array-item
      - any data-item
      - updated array-item with the new appended data-item


``insert``
^^^^^^^^^^

Add a new key-item-pair to an already existing map-item.


**Example**:

::

    - test_map = { "test": ["poi1", "poi2"]}

    print("test-output")
    - content = test_map.insert("asdf", test_map).get("asdf")

**Arguments**:

.. tabularcolumns:: |m{0.1\textwidth}|m{0.2\textwidth}|m{0.63\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Position**
      - **Type**
      - **Content**

    * - 1
      - string-value
      - key for the new item within the map

    * - 2
      - any data-item
      - new object, which should be added to the existing array


**Output Type**:

    map-item

**Input Item**:

.. tabularcolumns:: |m{0.1\textwidth}|m{0.2\textwidth}|m{0.2\textwidth}|m{0.40\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Item Type**
      - **Argument 1**
      - **Argument 2**
      - **Output Content**

    * - map-item
      - string-value
      - any data-item
      - updated map-item with the new iserted key-value-pair


``split``
^^^^^^^^^

Split a string-value into an array-item which contains the split content.

**Example**:

::

    - packages = "nano,vim"

    apt("install")  
    -> present:
        - packages = packages.split(",")

**Arguments**:

.. tabularcolumns:: |m{0.1\textwidth}|m{0.2\textwidth}|m{0.63\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Position**
      - **Type**
      - **Content**

    * - 1
      - string-value
      - Only a string of one single character to identify the position, where to split. If the string is longer, only the first character of the string is used. A special case is the line break, which consist of the characters "\n".


.. raw:: latex

    \newpage
    
    
**Output Type**:

    array-item

**Input Item**:

.. tabularcolumns:: |m{0.15\textwidth}|m{0.15\textwidth}|m{0.63\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Item Type**
      - **Argument**
      - **Output Content**

    * - string-value
      - string-value
      - array-item with the split content of the original string input


``get``
^^^^^^^

Get an element of an array or of a map.

**Example**:

::

    - packages = [ "nano", "vim" ]

    for(i = 0; i < packages.size(); i++)
    {
    	print("test-output")
    	- second_element = packages.get(i)
    }

**Arguments**:

.. tabularcolumns:: |m{0.1\textwidth}|m{0.2\textwidth}|m{0.63\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Position**
      - **Type**
      - **Content**

    * - 1
      - string-value
      - key to identify key-value pair within a map-item

    * - 1
      - int-value
      - position in map-item or array-item

**Output Type**:

    data-item

**Input Item**:

.. tabularcolumns:: |m{0.15\textwidth}|m{0.15\textwidth}|m{0.63\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Item Type**
      - **Argument**
      - **Output Content**

    * - map-item
      - string-alue
      - value, which belongs to the key, which match with the string of the argument

    * - map-item
      - int-value
      - data-item at the position of the inputnumber
 
    * - array-item
      - int-value
      - data-item at the position of the inputnumber



``contains``
^^^^^^^^^^^^

Check if an item contains another specific item.

**Example**:

::

    - packages = [ "nano", "vim" ]

    if(packages.contains("nano") == true)
    {
        ...
    }

**Arguments**:

.. tabularcolumns:: |m{0.1\textwidth}|m{0.2\textwidth}|m{0.63\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Position**
      - **Type**
      - **Content**

    * - 1
      - string-value
      - string, which should be checked

**Output Type**:

    bool-value

**Input Item**:

.. tabularcolumns:: |m{0.15\textwidth}|m{0.15\textwidth}|m{0.63\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Item Type**
      - **Argument**
      - **Output Content**

    * - map-item
      - string-value
      - result if the map contains a key, which match the argument string

    * - array-item
      - string-value
      - result if the array contains a value-item, which match the argument string

    * - string-value
      - string-value
      - result if the string contains a substring, which match the argument string


``parse_json``
^^^^^^^^^^^^

Parse a json-formated for easies access to the content

**Example**:

::

    - input = "{ \"test\": 2, \"asdf\": { \"xyz\": 42 } }"
    - parsed_content = {}

    item_update("parse json")
    - parsed_content = input.parse_json()


**Arguments**:

    no arguments

**Output Type**:

    data-item based on the parsed content

**Input Item**:

.. tabularcolumns:: |m{0.27\textwidth}|m{0.66\textwidth}|

.. list-table::
    :header-rows: 1

    * - **Item type**
      - **Output Content**

    * - string-item
      - json-formated string


.. raw:: latex

    \newpage
    