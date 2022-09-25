Loop calling
============

CPT3: An Integrated Package for ChIA-PET, HiChIP and PLAC-Seq data analysis.  

.. contents:: 
    :local:

Loop calling
-------------

CPT3 can obtained .

* CPT3 can calling loops with three different mode.

* 1. calling loops with ChIP-Seq peaks

.. code:: bash

    $ java -jar ChIA-PET.jar --INPUT_ANCHOR_FILE sample.peaks_narrowPeak \
     a file which contains user-specified anchors for interaction calling. If you don't have this \
     file, please specify the value of this variable as "null" instead. Default: null.

* 2. calling loops with MACS2 peak detect by CPT3

.. code:: bash

    $ java -jar ChIA-PET.jar --macs2 macs2 \
    macs2 path, using macs2 callpeak to detect anchor peak with alignment file

* 3. calling loops with SPP method
    $ java -jar ChIA-PET.jar \
    dont define --INPUT_ANCHOR_FILE and --macs2 paramaters.


.. tip:: For feature requests or bug reports please open an issue `on github <https://github.com/GuoliangLi-HZAU/ChIA-PET_Tool_V3>`__.
