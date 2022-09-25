PET divide
==========

CPT3: An Integrated Package for ChIA-PET, HiChIP and PLAC-Seq data analysis.  

.. contents:: 
    :local:

PET dividing
------------

CPT3 can divide paired reads into valid pair reads, self-ligation reads and other- pair reads based on interaction distance or 
restriction endonuclease sites and fragment.

* divide pair reads based on interaction genomic distance (valid for ChIA-PET and HiChIP data)
* divide pair reads based on restriction endonuclease sites and fragment (valid for in-situ ChIA-PET and HiChIP data)

.. code:: bash

    $ java -jar ChIA-PET.jar --SELF_LIGATION_CUFOFF 8000 \
    specifies the distance threshold between self-ligation PETs and intra- chromosomal inter-ligation PETs. \
    Default: 8000 for ChIA-PET data, 1000 for HiChIP data.


.. tip:: For feature requests or bug reports please open an issue `on github <https://github.com/GuoliangLi-HZAU/ChIA-PET_Tool_V3>`__.
