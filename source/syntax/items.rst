Items
-----

Items are the objects used to store any information inside the sakura-files. They could also be called variables.

Types
~~~~~

In this description all objects, which contain values, are called *items*. Any item in the sakura-files is written without explicit type. Internally the items are handled like JSON objects. So they can be values of different types, arrays of any other item or a key-item-map. In this regard it's similar to variables in Python. 

Overview of all available item types and their relation to each other:

::

    data-item
        │
        ├── map-item
        │
        ├── array-item
        │
        └── value-item
                │
                ├── string-value
                │
                ├── int-value
                │
                ├── float-value
                │
                └── bool-value


Based on this overview, if somewhere in the following document there is a reference to *value-item* for example, it can be a *string-value* or any other of the listed values. The same goes also for *data-items*, which could be replaced by any from the list. The data-item class is provided by the library *libKitsunemimiCommon*.

The value-items *int-value* and *float-value* are slightly special, because the *int-value* is internally a 64 bit long value and the *float-value* is internally a double value. So the allowed value range for these both types is bigger than the name implies.

Maybe in the future I will also introduce optional type definitions to allow only a specific type for a marked item.


Item Assignments
~~~~~~~~~~~~~~~~

Each item assignment in the sakura-files has in general the following style:

::

    - <ITEM> = <ITEM_OF_VALUE>

When an assignment is done like this, the item on the left side gets the type and the value of the item or value on the right side assigned.

To avoid checking line-breaks or indentation while parsing the code, like it is in Python, each assignment begins with a "-". It would be also possible to use a ";" at the end of each line, like it is done for example in C++, but in my opinion the "-" makes the syntax more beautiful and looks like a list of bullet points.


.. raw:: latex

    \newpage



The following assignment types are supported:

* assign undefined

    **Syntax**

    ::

        - <ITEM> = "{{}}"

    This is a special case. It's similar to initializing a variable with *None* in Python or with *nullptr* in C++ and means that the item has no defined state. (I don't exactly know anymore, why I used *{{}}* here. When I remember again, I will write it down here.)

    Before a sakura-file will be executed, it checks if all items have a defined values. This way it can be guaranteed that all items, which have no default-value, are set into a defined state by the instance which calls this sakura-file. 

    **Example**

    ::

        - uninit_value = "{{}}"


* assign values

    **Syntax**

    ::

        - <ITEM> = <VALUE>

    Based on the overview at the beginning of this section, a string, number or boolean can be assigned to turn the item into a value-item with the assigned content.

    **Example**

    ::

        - path = "/tmp/test_file"
        - answer = 42
        - answer_float = 42.0
        - is_true = true


* assign arrays and maps

    **example Syntax**

    ::

        - <ITEM> = { <VALUE> : [ <VALUE> , ...],  { <VALUE> :  ... }

        - <ITEM> = [ <VALUE> , [ <VALUE> , ... ], ... ]

    Similar to array, also complete map in json-style are possible to assign to an item. 

    **Restrictions**

    References to other items are not allowed in this definition. Only hardcoded int-values, float-values and string-values can be used. To add other existing items to an array-item or a map-item, used the *append* or *insert* functions (see later section).

    **Example**

    ::

        - test_array = [ "nano", "vim" ]
        - test_map = { "test": ["poi1", "poi2"]}


.. raw:: latex

    \newpage



* assign other items

    **Syntax**

    ::

        - <ITEM> = <ANOTHER_ITEM>

        - <ITEM> = <ANOTHER_ITEM>.<FUNCTION>(<ARGUMENT>)

    Similar to values other items can be assigned. Here the item on the left side will become a copy of the item on the right side. This can be also done with items with one or more function calls to temporarily change the content of the item before assigning it to the new item. More about the functions is written in a later sections.

    **Example**

    ::

        - packages = [ "nano", "vim" ]

        - packages_copy = packages
        - first_package = packages.get(0)


String Values
~~~~~~~~~~~~~

String values have a special feature, because all strings, which are assigned to a item, are handled as simple Jinja2 string. This functionality is provided by the library *libKitsunemimiJinja2*. 

The following three types are supported:

* replacements

    **Syntax**

    ::

        {{ <ITEM_NAME> }}


    **Example**

    :: 

        - test_item = "test-string"

        ...

        - message = "this is a {{test_item}}"

        (the item "message" now has the content: "this is a test-string")
        

* if-conditions

    **Syntax**

    ::

        {% if <ITEM_NAME> is <COMPARE_VALUE> %} ... {% else %} ... {% endif %}


    **Example**

    :: 

        - answer = 42
        - test_item = "test-string"

        ...

        - message = "this is {% if answer is 42 %}a {{ test_item }}{% endif %}"

        (the item "message" now has the content: "this is a test-string")



.. raw:: latex

    \newpage



* for-loops

    **Syntax**

    ::

        {% for <TEMP_VAR> in <ITEM_NAME> %} ... {{ <TEMP_VAR> }} ... {% endfor %}


    **Example**

    ::

        - packages = [ "nano", "vim" ]

        ...

        - package_string = "{% for single_p in packages %} {{ single_p }} {% endfor %}"

        (the item "package_string" now has the content: " nano  vim " as single string)


