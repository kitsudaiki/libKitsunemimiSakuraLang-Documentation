Files
-----

The script files are refered to in this document as *sakura-files*. The structure of these files will be shown according to the example from the beginning of this chapter:

**Example**

::

    ["test example file"]

    - packages = [ "nano", "vim" ]
    - path = "/tmp/test_file"
    - test_output = "{{}}"

    apt("update and install")  
    -> update
    -> present:
    - packages = packages

    # loop to print all packages-names
    for(package : packages)
    {
        print("print packages-names")
        - output = package
    }

    if(packages.size() == 2)
    {
        ini_file("get value from a test-ini-file")
        - file_path = path
        - group = "DEFAULT"
        - entry = "asdf"
        -> read:
            - blossom_output >> test_output
        -> set:
            - value = "123456789"

        print("print init-file-output")
        - first_try = test_output
    }


Each sakura-file consist of the following three parts:

* **Header**

    ::

        ["test example file"]

    The header of the file only contains a name for the file between "[]". This name is printed in the output and may help while debugging. With support for only one file, it doesn't make much sense currently but when support for nested sakura-files will be added in a future version, it will make debugging a little bit easier.

* **Global items**

    ::

        - packages = [ "nano", "vim" ]
        - path = "/tmp/test_file"
        - test_output = "{{}}"

    The global items are only global within this file, i.e. they are not visible outside this file. Each item, which is referenced in assignments within the file or used to write blossom_output back into a item, has to be defined here. The only exception here are counter items in for-loops.

.. raw:: latex

    \newpage


* **Body**

    ::

        apt("update and install")  
        -> update
        -> present:
        - packages = packages

        # loop to print all packages-names
        for(package : packages)
        {
            print("print packages-names")
            - output = package
        }
        
        if(packages.size() == 2)
        {
            ini_file("get value from a test-ini-file")
            - file_path = path
            - group = "DEFAULT"
            - entry = "asdf"
            -> read:
                - blossom_output >> test_output
            -> set:
                - value = "123456789"

            print("print init-file-output")
            - first_try = test_output
        }

    The body of the file consist of an arbitrary number of blossoms and blossom-groups, which are grouped by if-conditions, for-loops and parallel-sections.


.. raw:: latex

    \newpage
