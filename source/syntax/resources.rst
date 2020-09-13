Resources
---------

Resources are normal sakura-files. Unlike subtrees they are globaly accessable and are called like blossoms. They have two requirements:

1. They have to be stored inside os a *resoureces* directory beside the sakura-files

2. The name inside of the sakura-file between the *[]* has to be a single word based on characters and *_* only (whitespaces are NOT allowed here)

The resource can be called by a normal blosom-call:

::

	<RESOURCE_NAME>("some text for output")
	- <VAR1_IN> = <VAR>
	- <VAR2_OUT> >> <VAR>
	- ...

The *<RESOURCE_NAME>* is the name of the tree at the beginning of the sakura-file. Thats the reason, why this name doesn't allow whitespaces.

**Example**

File structure

::

	.
	├── resources
	│   └── test-resource.sakura
	│
	└── root.sakura


Content of `root.sakura`

::

	["resource-subtree-test"]
	- test_text = "this is a test"
	- output_resource = ""

	test_resource("call test-ressource")
	- test_text = test_text
	- new_text >> output_resource


Content of `test-resource.sakura`

::

	["test_resource"]
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

