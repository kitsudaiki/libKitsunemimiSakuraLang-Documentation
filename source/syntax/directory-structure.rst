Directory Structure
-------------------

The tool also provides the functionality to store files beside the sakura-files, which can be used by the blossoms. To use this the directory must have for following structure:

::

    .
    │
    ├── <SAKURA_FILE_1>
    ├── <SAKURA_FILE_2>
    ├── ...
    │
    ├── <SUB_DIRECTORY_1>
    │         ├── <SAKURA_FILE_1_1>
    │         ├── <SAKURA_FILE_1_2>
    │         ├── ...
    │         ├── files
    │         │     ├── <FILE_1>
    │         │     ├── <FILE_2>
    │         │     └── ...
    │         └── ...
    │
    ├── files
    │     ├── <FILE_1>
    │     ├── <FILE_2>
    │     └── ...
    │
    ├── resources
    │     ├── <RESOURCE_1>
    │     ├── <RESOURCE_2>
    │     └── ...
    │
    └── templates
          ├── <TEMPLATE_FILE_1>
          ├── <TEMPLATE_FILE_2>
          └── ...

Directories:

* **files**

    All files in this directory can be copied by the *copy*-blossom to another directory on the local disk.

* **resources**

    This directory contains global accessible sakura-failes, which can be called everywhere like a normal blossom-call.

* **templates**

    All Jinja2 template files stored in here can be used by the *template*-blossom to fill them with items to generate text files.


The *files* and *templates* directories always have to be in the same directory like the sakura-files, which is using them. 

.. raw:: latex

    \newpage

