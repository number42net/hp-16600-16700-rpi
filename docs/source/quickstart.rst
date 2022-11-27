Quickstart
==========

The following is a short description of how to connect to an HP 16600 / 16700 logic analyzer, set-up some basic configuration and collect data

Prerequisites
-------------

    * Make sure that your HP logic analyzer is powered-on, and you have a running GUI session
    * It's not possible to connect to the RPI interface when no GUI session is active
    * The RPI interface should be enabled by default, but you can get more information on how to enable it in the user guide

    * If you're having connection issues, try connecting via telnet on port 6500

Establishing a connection
-------------------------

The first step is to connect to the logic analyzer:


    >>> c = LogicAnalyzer("192.168.0.20")

Next, get a list a logic analyzer modules in the frame and use the first:

    >>> modules = c.get_modules()
    >>> analyzer = modules[0]

Basic configuration
-------------------

Now that we have a logic analyzer module selected, we can perform some basic configuration:

    >>> analyzer.set_pods("A1,A2")
    >>> analyzer.set_label("ADDR", "A1[15:0]")
    >>> analyzer.set_label("DATA", "A2[7:0]")

    >>> analyzer.set_trigger("ADDR=#hFFXX")
    >>> analyzer.set_mode("stnorn")

Once the logic analyzer has been configured, we can start it and poll its status

    >>> analyzer.start()
    >>> analyzer.running()
    True
    >>> analyzer.running()
    False

Collecting data
---------------

Now that it's finished, we can collect the data


    >>> analyzer.get_listing()
           State Number           Time  Address  Data
    0            -32768 -3276799901696      191     0
    1            -32767 -3276699901699      191     0
    2            -32766 -3276599901702      191     0
    3            -32765 -3276499901705      191     0
    4            -32764 -3276399901708      191     0
    ...             ...            ...      ...   ...
    65531         32763  3276299901711      191     0
    65532         32764  3276399901708      191     0
    65533         32765  3276499901705      191     0
    65534         32766  3276599901702      191     0
    65535         32767  3276699901699      191     0
