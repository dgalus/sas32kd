SAS Listener Library examples
-----------------------------

Library to attach own actions on SAS event occurences.

|


**Import library:**

.. code-block:: python

  from sas32kd import Sas32kdListener

|

**Connect to SAS audio router TCP/IP Server Module:**

.. code-block:: python

   sas = Sas32kdListener(ip="10.10.10.10", port=1270)

Port is optional arguments.

|


**Disconnecting from TCP/IP Server Module:**

.. code-block:: python

   sas.disconnect()

|

**Attach action on opto turned on:**
*on_opto_turned_on(opto_num: int, func, *args, **kwargs)*

.. code-block:: python

   def func(arg):
     print("OPTO ON " + str(arg))

   sas.on_opto_turned_on(222, func, "some argument")

- opto_num: Opto number.
- func: Function.
- args: Function args.
- kwargs: Function kwargs.

|

**Attach action on opto turned off:**
*on_opto_turned_off(opto_num: int, func, *args, **kwargs)*

.. code-block:: python

   def func(arg):
     print("OPTO OFF " + str(arg))

   sas.on_opto_turned_off(222, func, "some argument")

- opto_num: Opto number.
- func: Function.
- args: Function args.
- kwargs: Function kwargs.

|

**Attach action on relay turned on:**
*on_relay_turned_on(relay_num: int, func, *args, **kwargs)*

.. code-block:: python

   def func(arg):
     print("RELAY ON " + str(arg))

   sas.on_relay_turned_on(222, func, "some argument")

- relay_num: Relay number.
- func: Function.
- args: Function args.
- kwargs: Function kwargs.

|

**Attach action on relay turned off:**
*on_relay_turned_off(relay_num: int, func, *args, **kwargs)*

.. code-block:: python

   def func(arg):
     print("RELAY OFF " + str(arg))

   sas.on_relay_turned_off(222, func, "some argument")

- relay_num: Relay number.
- func: Function.
- args: Function args.
- kwargs: Function kwargs.

|

**Attach action on take:**
*on_take(self, inp: int, outp: int, func, *args, **kwargs)*

.. code-block:: python

   def func(arg):
     print("TAKE " + str(arg))

   sas.on_take(222, 333, func, "some argument")

- inp: Input number.
- outp: Output number.
- func: Function.
- args: Function args.
- kwargs: Function kwargs.

|

**After attaching functions, execute run() function!**

.. code-block::

   sas.run()