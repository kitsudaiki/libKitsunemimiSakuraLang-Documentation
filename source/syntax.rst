Syntax
======

For this tool a new script language was created. In my opinion something like YAML, which is used in Ansible, is too limited for something like conditionals or loops and bigger languages like Ruby, which is used by Chef, are too powerful and complex for an automation tool. 

A tool for automating processes has its own requirements and limitations and so it also need its own script language. Thats why a new one was created with some syntax inspiration of C++, Python and YAML.


**Simple example**

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



**Restrictions**

In this version 0.2.0 only single files can be executed by the tool. The functionality that files can call other files is expected to be added in version 0.3.0.


.. raw:: latex

    \newpage


.. include:: syntax/general_syntax.rst
.. include:: syntax/items.rst
.. include:: syntax/blossoms-and-blossom-groups.rst
.. include:: syntax/file-structure.rst
.. include:: syntax/directory-structure.rst
.. include:: syntax/functions.rst
