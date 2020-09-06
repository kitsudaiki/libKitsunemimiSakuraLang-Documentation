``for``
-------

for-loop
~~~~~~~~

Simple for-loop to iterate over a specific range of numbers.

**Syntax**

::

    for( <ITEM_NAME> = <START_VALUE> ; <ITEM_NAME> < <END_VALUE>; <ITEM_NAME> ++ )
    {
        ...
    }

The *<ITEM_NAME>* can be arbitrary. It has by default an int-value as type. Thats why *<START_VALUE>* and *<END_VALUE>* also have to be int values or items with a function call, which return an int-value like in the example below. The *<ITEM_NAME>* can be used as counter-item inside the loop, for example to request items with a get-call.

**Example**

::

    - packages = [ "nano", "vim" ]

    for(i = 0; i < packages.size(); i++)
    {
        print("print name")
        - name = packages.get(i)
    }


**Restrictions**

    * only "<" is available as compare-type (update with version 0.4.0)

    * the arithmetic operation "++" is a bit of a fake. Is still hard-coded in the parser. Because of this something like "i--" or "i=i+2" is not possible. (update with version 0.4.0)


for-each-loop
~~~~~~~~~~~~~

Iterate over all elements of an array-item or a map-item.

**Syntax**

::

    for( <ITEM_NAME> : <MAP_OR_ARRAY_ITEM> )
    {
        ...
    }

The *<ITEM_NAME>* can is arbitrary. It has the type the value of the current position inside the array or map, which should be iterated and is accessible as normal variable inside the for-loop.

**Example**

::

    - packages = [ "nano", "vim" ]

    for(package : packages)
    {
        print("print name")
        - name = package
    }


.. raw:: latex

    \newpage
    