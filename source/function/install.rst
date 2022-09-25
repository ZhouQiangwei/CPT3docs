Installation
=============

CPT3: An Integrated Package for ChIA-PET, HiChIP and PLAC-Seq data analysis.  

.. contents:: 
    :local:

Requirements
-------------

* JDK>=1.8(https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* BWA(http://bio-bwa.sourceforge.net/)
* SAMtools(http://samtools.sourceforge.net/)
* BEDTools(https://bedtools.readthedocs.io/en/latest/)
* R(https://www.r-project.org/)
* R package grid(install.packages("grid"))
* R package xtable(install.packages("xtable"))
* R package RCircos(install.packages("RCircos"))
* `fastp, raw reads as input need <https://github.com/OpenGene/fastp>`_.

The details of requirements can see :doc:`Requirements`

Install
-------
.. code:: bash

    a) git clone git@github.com:GuoliangLi-HZAU/ChIA-PET_Tool_V3.git
    b) Change directory into the top directory of ChIA-PET_Tool_V3
	$ cd ChIA-PET_Tool_V3
    c) Type 
	$ java -jar ChIA-PET.jar --help

.. tip:: For feature requests or bug reports please open an issue `on github <https://github.com/GuoliangLi-HZAU/ChIA-PET_Tool_V3>`__.
