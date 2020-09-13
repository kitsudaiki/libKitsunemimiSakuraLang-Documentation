Blossoms and Blossom-Groups
---------------------------

Because the tool *SakuraTree* is a reference for trees with cherry blossoms, the core objects of this automation tool are called blossoms. They are a predefined set, which can be called within the sakura-files. They process the desired tasks and are filled with values via item assignments. Most of them consist of a blossom-group, which contains one ore more blossoms:

**Example**

::

    - test_input = "poi"
    - test_output = "{{}}"

    ini_file("get value from a test-ini-file and writ into file: {{test_input}}")
    - file_path = "/tmp/test_file"
    - group = "DEFAULT"
    - entry = "asdf"
    -> read:
        - value >> test_output
    -> set:
        - value = test_input


The whole construct has up to 5 different parts:

* **Blossom-group definition**

    Syntax:

    ::

        <BLOSSOM_GROUP_TYPE_NAME> ( <IDENTIFIER_STRING_FOR_DEBUG_OUTPUT> )

    The first is the definition of the blossom-group. *<BLOSSOM_GROUP_TYPE_NAME>* identifies the type, which has to be selected from the predefined set. In the example it is *ini_file* in order to read and change INI files. Within the following "( ... )" an identifier string is required, which is printed in log output for easier debugging. This string is handled as jinja2-string. That way the name can be filled with additional internal information (see available jinja2 rules in the string-value section). As input for the jinja2-string all within the file global accessable items or counter value-items of a loop can be used. Thats make the output more unique especially for blossom-groups within loop. 

    Example:

    ::

        ini_file("get value from a test-ini-file and writ into file: {{test_input}}")


* **Blossom-group input**

    After the definition of the blossom-group the group-items are defined. These are normal item assignment like in the item section. These items are visible for all blossoms, which are defined in the very same blossom-group. That way it's possible to run multiple blossoms against the same file, while setting the path of the file only one time, for example. 

    Blossom-group-items are not required and can also be empty.

    Example:

    ::

        - file_path = "/tmp/test_file"
        - group = "DEFAULT"
        - entry = "asdf"


* **Blossom definition**
    
    Syntax:

    ::

        -> <BLOSSOM_TYPE_NAME>

        -> <BLOSSOM_TYPE_NAME> :

    Like the blossom-groups also the blossom-type has to be selected from a list of predefined blossoms. Like shown in the syntax, it has to start with a "->". That way it can not be mixed with item assignments of blossom-group definitions. If input items or an output should be defined in the blossom-part, a ":" has to be appended after the type name. If no items are following, this character should not be set. Note: this ":" syntax rule may be deprecated at any point in the future; it's a leftover of the first syntax iteration.

    Example:

    ::

        -> set:


* **Blossom input**

    After the definition of the blossom was done, more item assignments may follow. The items here are only visible to this blossom. Here all required items have to be set, which are not already set by the blossom-group items. 

    Example:

    ::

        - value = test_input


* **Blossom output**

    Syntax:

    ::

        - <OUTPUT_VALUE> >> <ITEM>

    Some blossoms provide an output. See the blossom definitions to see if the blossom has an output. If there is output, it can be written back into an item, which already exists in the items declaration at the beginning of the file. This way the content of the output can be used by another blossom.

    Example:

    ::

        - value >> test_output



**special case**

There are also some special types with no separation in blossom and blossom-group and look like the following example:

::

    print("print test-string")
    - test_output = "this is a test-string"

Input and output is handled the same way like in the normal case.



.. raw:: latex

    \newpage

