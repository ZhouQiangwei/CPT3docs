Linker filter
=============

CPT3: An Integrated Package for ChIA-PET, HiChIP and PLAC-Seq data analysis.  

.. contents:: 
    :local:

Linker filter
-------------

We provide auto linker detect and filtering function in CPT3.

* quality control for raw sequencing ChIA-PET, HiChIP and PLAC-Seq data
* Linker filtering for ChIA-PET data and BL-HiChIP data

.. code:: bash

    $ java -jar ChIA-PET.jar --autolinker true \
    detect linker by our program, true [default] or false, then no need provide --linker and --mode paramater.



.. tip:: For feature requests or bug reports please open an issue `on github <https://github.com/GuoliangLi-HZAU/ChIA-PET_Tool_V3>`__.
