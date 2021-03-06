.. _mock-asserter:

mock
****

This is the asserter for mocks.

.. code-block:: php

   <?php
   $mock = new \mock\MyClass;

   $this
       ->mock($mock)
   ;

.. note::
   Refer to the documentation on :ref:`mock <les-bouchons-mock>` for more information on how to create and manage mocks.


.. _call-anchor:

call
====

``call`` let you specify which method of the mock to check, his call must be followed by a call to one of the following verification method like `atLeastOnce`_, `once/twice/thrice`_, `exactly`_, etc...

.. code-block:: php

   <?php

   $this
       ->given($mock = new \mock\MyFirstClass)
       ->and($object = new MySecondClass($mock))

       ->if($object->methodThatCallMyMethod())  // This will call myMethod from $mock
       ->then

       ->mock($mock)
           ->call('myMethod')
               ->once()
   ;

.. _at-least-once:

atLeastOnce
```````````

``atLeastOnce`` check that the tested method (see :ref:`call <call-anchor>`) from the mock has been called at least once.

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->call('myMethod')
               ->atLeastOnce()
   ;

.. _exactly-anchor:

exactly
```````

``exactly`` check that the tested method (see :ref:`call <call-anchor>`) has been called a specific number of times.

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->call('myMethod')
               ->exactly(2)
   ;

.. _never-anchor:

never
`````

``never`` check that the tested method (see :ref:`call <call-anchor>`) has never been called.

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->call('myMethod')
               ->never()
   ;

.. note::
   ``never`` is equivalent to ``:ref:`exactly <exactly-anchor>`(0)``.


.. _once-twice-thrice:

once/twice/thrice
`````````````````
This asserters check that the tested method (see :ref:`call <call-anchor>`) from the tested mock has been called exactly:

* once
* twice
* thrice

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->call('myMethod')
               ->once()
           ->call('mySecondMethod')
               ->twice()
           ->call('myThirdMethod')
               ->thrice()
   ;

.. note::
   ``once``, ``twice`` and ``thrice`` are respectively equivalent to ``:ref:`exactly <exactly-anchor>`(1)``, ``:ref:`exactly <exactly-anchor>`(2)`` and ``:ref:`exactly <exactly-anchor>`(3)``.


.. _with-any-arguments:

withAnyArguments
````````````````

``withAnyArguments`` allow to check any argument, non-specified, when we call the tested method (see :ref:`call <call-anchor>`) of the tested mock.

This method is useful to reset the arguments of the tested method, like in the following example:

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->call('myMethod')
               ->withArguments('first')     ->once()
               ->withArguments('second')    ->once()
               ->withAnyArguments()->exactly(2)
   ;

.. _with-arguments:

withArguments
`````````````

``withArguments`` let you specify the expected arguments that the tested method should receive when called (see :ref:`call <call-anchor>`).

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->call('myMethod')
               ->withArguments('first', 'second')->once()
   ;

.. warning::
   | ``withArguments`` does not check the arguments type.
   | If you also want to check the type, use :ref:`withIdenticalArguments <with-identical-arguments>`.


.. _with-identical-arguments:

withIdenticalArguments
``````````````````````

``withIdenticalArguments`` let you specify the expected arguments that tested method should receive when called (see :ref:`call <call-anchor>`).

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->call('myMethod')
               ->withIdenticalArguments('first', 'second')->once()
   ;

.. warning::
   | ``withIdenticalArguments`` checks the arguments type.
   |  If you do not want to check the type, use :ref:`withArguments <with-arguments>`.


.. _was-called:

wasCalled
=========

``wasCalled`` checks that at least one method of the mock has been called at least once.

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->wasCalled()
   ;

.. _was-not-called:

wasNotCalled
============

``wasNotCalled`` checks that no method of the mock has been called.

.. code-block:: php

   <?php
   $mock = new \mock\MyFirstClass;

   $this
       ->object(new MySecondClass($mock))

       ->mock($mock)
           ->wasNotCalled()
   ;
