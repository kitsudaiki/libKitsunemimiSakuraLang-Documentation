``parallel_for``
----------------

With this section-type it's possible to spread the workload of a for-loop over multiple threads. The ``parallel_for`` is exactly like the name implies, a mix of ``parallel`` and ``for``.

In the *parallel_for* each iteration will be encapsulated as standalone object with the whole content of the loop as a new subtree and all incoming values in addition to the item at the current location of the iterated array or map or the counter item respectively. This object is placed in a queue from where it will be processed by a free worker thread. That way even in case of a loop over an item with 1000 entries this doesn't create 1000 threads but instead of this it places 1000 objects into the subtree-queue to be processed by x worker threads.

Exactly like in the *parallel*-section, changing values inside the parallel-loop doesn't affect any value in any other iteration of the loop and doesn't affect values outside the loop. Besides this, everything following the for-loop inside the sakura-file is only executed after each iteration of the loop was fully processed by the worker threads.


parallel for-loop
~~~~~~~~~~~~~~~~~

Parallel version of a for-loop to iterate over a specific range of numbers.

**Syntax**

::

    parallel_for( <ITEM_NAME> = <START_VALUE> ; <ITEM_NAME> < <END_VALUE>; <ITEM_NAME> ++ )
    {
        ...
    }


The *<ITEM_NAME>* can be arbitrary. It has by default an int-value as type. Thats why *<START_VALUE>* and *<END_VALUE>* also have to be int-values or items with a function call, which return an int-value like in the example below. The *<ITEM_NAME>* can be used as counter item inside the loop, for example to request items with a get-call.

**Example**

::

    - packages = [ "nano", "vim" ]

    parallel_for(i = 0; i < packages.size(); i++)
    {
        print("print name")
        - name = packages.get(i)
    }


**Restrictions**

    * only "<" is available as compare-type (to be extended with version 0.4.0)

    * the arithmetic operation "++" is a bit of a fake. It is still hard-coded in the parser. Because of this something like "i--" or "i=i+2" is not possible. (update to be expected with version 0.4.0)

    * no results from inside the parallel-loop can be written back into a item outside the loop or sended to another iteration (update to be expected with version 0.3.0)

    
parallel for-each-loop
~~~~~~~~~~~~~~~~~~~~~~

Parallel version of a loop to iterate over all elements of an array-item or a map-item.

**Syntax**

::

    parallel_for( <ITEM_NAME> : <MAP_OR_ARRAY_ITEM> )
    {
        ...
    }

The *<ITEM_NAME>* can be arbitrary. It has the type the value of the current position inside the array or map, which should be iterated and is accessble as normal item inside the for-loop.

**Example**

::

    - packages = [ "nano", "vim" ]

    parallel_for(package : packages)
    {
        print("print name")
        - name = package
    }

**Restrictions**

    * no results from inside the parallel-loop can be written back into a item outside the loop or send to another iteration (update to be expected with version 0.3.0)



.. raw:: latex

    \newpage
    

post aggreation
~~~~~~~~~~~~~~~

Sometime it is necessary to get information out of the loop. To make this possible in the case of a parallel executed loop without race-contition, there was the feature of a post-aggregation added. This make it possible to collect data from the loop at the end. The result is an object, where each entry contains the value of another cycle. This way, its is possible to collect the data and process them after the loop.

**General syntax:**

The post-aggregation has to be defined directly after the *parallel_for*.

::

    - <OUTPUT_ARRAY> = []

    parallel_for(<ITEM> : <ITEM_LIST>)
    - <OUTPUT_ARRAY> = <OUTPUT_ARRAY>.<OPERATION>(<SOME_ITEM>)   # <- post-aggregation
    {
        ...
    }

*<OPERATION>* can be *append* or *insert*. It also works for both types of *parallel_for*.


**Example**

::

    - input = ["asdf", "xyz", "poi"]
    - result = []
    - tempValue = ""

    parallel_for(value : input)
    - result = result.append(tempValue)
    {
        item_update("update value")
        - tempValue = ">{{value}}<"
    }

    print("print result")
    - output = result


Result of this example is:

::

    +-----------+---------------+
    | Item-Name | Value         |
    +===========+===============+
    | output    | [             |
    |           |     ">asdf<", |
    |           |     ">xyz<",  |
    |           |     ">poi<"   |
    |           | ]             |
    +-----------+---------------+


.. raw:: latex

    \newpage
    
