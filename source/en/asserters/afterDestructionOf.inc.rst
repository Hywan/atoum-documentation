.. _after-destruction-of:

afterDestructionOf
******************

It's the assertion that is dedicated to object destruction.

This assertion verifies that the given object is valid and check if ``__destruct()`` method is defined and then invokes it.

If ``__destruct()`` exists and is executed without any error or exception then the test succeeds.

.. code-block:: php

   <?php
   $this
       ->afterDestructionOf($objectWithDestructor)     // succeed
       ->afterDestructionOf($objectWithoutDestructor)  // fails
   ;
