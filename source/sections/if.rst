``if``
------

If-conditions are basically like they are known in C++:

**Syntax**

::

    if( <ITEM_TO_COMPARE> <COMPARE_TYPE> <ITEM_FOR_COMPARE> )
    {
        ...
    }
    else
    {

    }

They have still a huge amount of restrictions like shown below, but provide basic functionality. A comparison inside the if-condition has an item on the left and an item on the right side. Both sides can be hard-coded values, items or items with function calls like shown in the example. At the moment it can be compare all with all. After inserting the item content and processing all function calls, the remaining content is interpreted as string. Because of this a string-value can also be compared with a map-item or something like *if("2" == 2)* would also work and return a true result. So only the string-converted content of both sides is compared. Thats the main reason why only "==" and "!=" are supported as compare types at the moment.

**Example**

::

    - packages = [ "nano", "vim" ]
    - test_output = "test"

    if(packages.size() == 2)
    {
        assert("test-assert")
        - test_output == "test"
    }


**Restrictions**

    * only "==" and "!=" are supported as compare types (to be changed with version 0.3.0)

    * even if the value to check returns a bool-value, something like " == true " is still necessary (to be changed with version 0.3.0)

    * no "elseif" or something like this available (to be changed with version 0.3.0)

    * no binary operations available like "&&" or "||" to combine multiple conditions (to be changed with version 0.3.0 or 0.4.0)

.. raw:: latex

    \newpage
    