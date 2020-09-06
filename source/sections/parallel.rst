``parallel``
------------

The **parallel**-section can be used for simple multi-threading. 

**Syntax**

::

    parallel()
    {
        ...
    }

There is no content to be placed between "()". For each blossom, if-condition or something else, which is put directly in the inside the "{}", will be running in a separate thread. For each entry inside the "{}" a container is created with the subtree and all incoming values, which is then subsequently placed into a queue from where it will taken by the worker threads. 

If there is for example an if-condition with multiple blossoms inside the parallel-section, only the if-condition together with its whole content is packed as one subtree-container. So in the example below, only two subtrees are isolated in containers and processed by two worker threads, despite there being a total of three blossoms inside the parallel-section

In the case that something exist after the parallel-section, this will be executed only when all subtrees inside the parallel-section are completed. So the *print("test_output4")* in the example below would only execute after the other three prints inside the parallel-sections have printed their content.

**Example**

::

    - test_val = "test"
    - test_val2 = "test"

    parallel()
    {
        print("test_output1")
        - output = test_val

        if(test_val == test_val2)
        {
            print("test_output2")
            - output = test_val2

            print("test_output3")
            - output = test_val2
        }
    }
    
    print("test_output4")
    - output = test_val2

**Restrictions**

* All inside the parallel-section is an encapsulated universe. That means even when a blossom inside the if-condition in the example would write something into *test_val* or *test_val2*, the changes are only visible inside the worker thread. Values which changed inside the single threads of a parallel-section, are only visible inside the corresponding threads. All other threads and everything that will be executed after the parallel-section, is totally unaffected. (to be updated with version 0.3.0)

* At the moment the syntax doesn't provide any mutex functionality. So you have to make sure that threads don't try to edit the same file or something similar concurrently. (update expected with version 0.3.0 or 0.4.0)


.. raw:: latex

    \newpage

