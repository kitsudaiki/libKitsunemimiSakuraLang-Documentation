Directory Structure
-------------------

The tool also provides the functionality to store files beside the sakura-files, which can be used by the blossoms. To use this the directory must have for following structure:

::

    .
    │
    ├── <TREE_FILE_1>
    │
    ├── <TREE_FILE_2>
    │
    ├── ...
    │
    ├── files
    │     │
    │     ├── <FILE_1>
    │     │
    │     ├── <FILE_2>
    │     │
    │     └── ...
    │
    └── templates
            │
            ├── <TEMPLATE_FILE_1>
            │
            ├── <TEMPLATE_FILE_2>
            │
            └── ...

Directories:

* **files**

    All files in this directory can be copied by the *copy*-blossom to another directory on the local disk.

* **templates**

    All Jinja2 template files stored in here can be used by the *template*-blossom to fill them with items to generate text files.


The *files* and *templates* directories always have to be in the same directory like the sakura-files, which is using them. Even in the planned multi-file-support in version 0.3.0, there will most likely be no global files- or templates-directory, like it is in Ansible or Chef. 

.. raw:: latex

    \newpage

