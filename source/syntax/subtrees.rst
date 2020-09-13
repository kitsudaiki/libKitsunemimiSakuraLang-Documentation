Subtrees
--------

Subtrees are named sakura-files, which are called by other sakura-files. The value input and output are the same like for blossoms. They are called by its relative file-path, based on the path of the file, which calles the subtree.

General call of subtrees:

::

    subtree(<PATH_TO_SUBTREE>)
    - <VAR1_IN> = <VAR>
    - <VAR2_OUT> >> <VAR>
    - ...

If the *<PATH_TO_SUBTREE>* is the path to a directory instead of a file, it search for a file named *root.sakura* within the directory ane execute this file as next. The called file can be in the same directoy, like the file, which calls the subtree, or it can be in a sub-directory.


**Example**

File structure

::

    .
    ├── next
    │   └── subtree.sakura
    │
    └── root.sakura


Content of `root.sakura`

::

    ["resource-subtree-test"]
    - test_text = "this is a test"
    - output_resource = ""
    - output_subtree = ""

    subtree("next/subtree.sakura")
    - test_text = test_text
    - new_text >> output_subtree


Content of `test-resource.sakura`

::

    ["subtree test"]
    - test_text = "{{}}"
    - new_text = ""

    text_file("write into a text-file")
    - file_path = "/tmp/ressource-subtree-test"
    -> write:
        - text = test_text
    -> read:
        - text >> test_text


    item_update("change output for better test")
    - new_text = "asdf: {{test_text}}"


.. raw:: latex

    \newpage
