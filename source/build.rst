Build Project
=============

SakuraTree
----------

Requirements
~~~~~~~~~~~~

Environment
^^^^^^^^^^^

Operation System: **Linux**

Architecture: **x86_64** (**ARM** should work as well, because no fancy stuff is used, but this still was not tested)

Required Tools
^^^^^^^^^^^^^^

.. tabularcolumns:: |m{0.11\textwidth}|m{0.11\textwidth}|m{0.1\textwidth}|m{0.58\textwidth}|

.. list-table::
    :header-rows: 1

    * - **name**
      - **repository**
      - **version**
      - **task**

    * - g++
      - g++
      - >= 6.0
      - Compiler for the C++ code.

    * - make
      - make
      - >= 4.0
      - Process the make-file, which is created by qmake to build the programm with g++

    * - qmake
      - qt5-qmake
      - >= 5.0
      - This package provides the tool qmake, which is similar to cmake and create the Makefile for compilation.

    * - FLEX
      - flex
      - >= 2.6
      - Build the lexer code for all used parsers.

    * - GNU Bison
      - bison
      - >= 3.0
      - Build the parser code together with the lexer code.

    * - xxd
      - xxd
      - >= 1.10
      - converts text files into source code files


Installation on Ubuntu/Debian:

::

    sudo apt-get install g++ make qt5-qmake bison flex xxd


.. raw:: latex

    \newpage
    
Required Libraries
^^^^^^^^^^^^^^^^^^

Official Libraries
''''''''''''''''''

.. tabularcolumns:: |m{0.22\textwidth}|m{0.1\textwidth}|m{0.6\textwidth}|

.. list-table::
    :header-rows: 1

    * - **repository-name**
      - **version**
      - **task**
 
    * - libssl-dev
      - >= 1.1.0
      - For tls-encrypted data-transfer.

    * - libboost-filesystem-dev
      - >= 1.60
      - Used for file interactions like for example listing files in a directory or check if a path exist.

Installation on Ubuntu/Debian:

::

    sudo apt-get install libssl-dev libboost-filesystem-dev


Kitsunemimi Libraries
'''''''''''''''''''''

These repositories will be downloaded automatically by the build script of the tool itself (see next section). This list here is only as information to give an overview of all used Kitsunemimi libraries in this project.

.. tabularcolumns:: |m{0.27\textwidth}|m{0.06\textwidth}|m{0.6\textwidth}|

.. list-table::
    :header-rows: 1

    * - **repository-name**
      - **tag**
      - **download-path**

    * - libKitsunemimiCommon
      - v0.15.1
      - https://github.com/kitsudaiki/libKitsunemimiCommon.git 

    * - libKitsunemimiPersistence
      - v0.10.0
      - https://github.com/kitsudaiki/libKitsunemimiPersistence.git 

    * - libKitsunemimiArgs
      - v0.2.0
      - https://github.com/kitsudaiki/libKitsunemimiArgs.git 

    * - libKitsunemimiJson
      - v0.10.3
      - https://github.com/kitsudaiki/libKitsunemimiJson.git 

    * - libKitsunemimiJinja2
      - v0.7.3
      - https://github.com/kitsudaiki/libKitsunemimiJinja2.git 

    * - libKitsunemimiIni
      - v0.4.4
      - https://github.com/kitsudaiki/libKitsunemimiIni.git 

    * - libKitsunemimiNetwork
      - v0.6.4
      - https://github.com/kitsudaiki/libKitsunemimiNetwork.git 

    * - libKitsunemimiProjectNetwork
      - v0.2.0
      - https://github.com/kitsudaiki/libKitsunemimiProjectNetwork.git 

    * - libKitsunemimiSakuraNetwork
      - v0.1.0
      - https://github.com/kitsudaiki/libKitsunemimiSakuraNetwork.git 

    * - libKitsunemimiSakuraLang
      - v0.3.1
      - https://github.com/kitsudaiki/libKitsunemimiSakuraLang.git 


.. raw:: latex

    \newpage
    
Build
~~~~~

In all of my repositories you will find a *build.sh*. You only have to run this script. It doesn't require sudo, because you have to install the required tools manually beforehand, for example via apt. But if other projects of mine are required, it downloads them from GitHub and builds them in the correct version too. This script is also used by the CI pipeline, so it's tested with every commit.

Before running the build script:
::

    .
    └── SakuraTree
        ├── build.sh
        └── ...

After running the build script:
::

    .
    ├── build
    │   ├── libKitsunemimiCommon
    │   │   └── ...
    │   ├── libKitsunemimiPersistence
    │   │   └── ...
    │   └── ...
    │
    ├── libKitsunemimiCommon
    │   └── ...
    ├── libKitsunemimiPersistence
    │   └── ...
    ├── ...
    │
    ├── SakuraTree
    │   ├── build.sh
    │   └── ...
    │
    └── result
        └─── SakuraTree

It automatically creates a build and result directory in the directory where you have cloned the project. At first it builds all into the build directory and after all build steps are finished, it copies the final binary into the result directory.

The build script links all Kitsunemimi libraries statically into the final binary.

Tested on Debian and Ubuntu. If you use CentOS, Arch, etc and the build script fails on your machine, then please write me a message or file a GitHub issue and I will try to fix the script.
