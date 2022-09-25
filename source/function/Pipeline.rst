Pipeline
========

.. tip:: CPT3 can perform one click analysis or the following modules step by step:

    * :doc:`Linkerfilter`
    * :doc:`Alignment`
    * :doc:`PETdivide`
    * :doc:`peakcall`
    * :doc:`loopcall`
    * :doc:`visulization`

.. contents:: 
    :local:

+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
| tool                    | input files                        | main output file(s)              | main application                                                       |
+=========================+====================================+==================================+========================================================================+
|:doc:`Linkerfilter`      | Single/Paired-end fastq/gz files   | clean PETs after linker filter   | Perform Linker filter and qulaity contril for sequencing raw data      |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`Alignment`         | clean fastq file                   |  align sam/bam file              | Perform Single-end alignment and perform paired                        |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`PETdivide`         | aligned paired-end reads           | valid pairs reads, self-ligation | Dividing aligned pair reads into different categories                  |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`peakcall`          | valid pair reads                   | enrichment peak                  | Perform peak calling with MACS2 or SPP method                          |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+
|:doc:`loopcall`          | valid pair reads and peak results  | valid loops                      | Perform loop calling analysis                                          |
+-------------------------+------------------------------------+----------------------------------+------------------------------------------------------------------------+


CPT3 pipeline
^^^^^^^^^^^^^

An easy-to-use, auto-run package for ChIA-PET, HiChIP data analyses:

Raw reads:

.. code:: bash

    java -jar ChIA-PET.jar --fastq1 test_long_1.fastq.gz --fastq2 test_long_2.fastq.gz \
        --minimum_linker_alignment_score 14 --GENOME_INDEX hg38.fa --GENOME_LENGTH 3E9 \
        --CHROM_SIZE_INFO ChIA-PET_Tool_V3/chromInfo/hg38.chromSize.txt \
        --CYTOBAND_DATA ChIA-PET_Tool_V3/chromInfo/hg19_cytoBandIdeo.txt --SPECIES 1 \
        --output test_long --prefix GM12878 --thread 8 --fastp fastp

Or clean reads:

.. code:: bash

    java -jar ChIA-PET.jar --fastq1 test_long_1.fastq.gz --fastq2 test_long_2.fastq.gz \
        --minimum_linker_alignment_score 14 --GENOME_INDEX hg38.fa --GENOME_LENGTH 3E9 \
        --CHROM_SIZE_INFO ChIA-PET_Tool_V3/chromInfo/hg38.chromSize.txt \
        --CYTOBAND_DATA ChIA-PET_Tool_V3/chromInfo/hg19_cytoBandIdeo.txt --SPECIES 1 \
        --output test_long --prefix GM12878 --thread 8

With our test, we strong suggest --fastp paramater for analysis:

You can always see all available command-line options via --help:

.. code:: bash

    $ java -jar ChIA-PET.jar --help

- After the program runs successfully, a series of files with '-o' as prefix and report file will be generated in the output directory. Please refer to the doc for the specific output file and format details. 
- In addition, there will be an HTML report file containing basic information and statistical results of data analysis.

CPT3 pipeline main parameters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


+---------------------+--------------------------------------------------------------------------+
| **[ Main paramaters ]**                                                                        |
+=====================+==========================================================================+
| System.out.println("Usage: java -jar <path of ChIA_PET.jar> [options]                          |
+------------------------------------------------------------------------------------------------+
| Necessary options:                                                                             |
+---------------------+--------------------------------------------------------------------------+
| --fastq1            | path of read1 fastq file                                                 |
+---------------------+--------------------------------------------------------------------------+
| --fastq2            | path of read2 fastq file                                                 |
+---------------------+--------------------------------------------------------------------------+
| --autolinker        | detect linker by our program, then no need provide --linker and --mode   |
|                     | paramater.                                                               |
+---------------------+--------------------------------------------------------------------------+
| --mode              | mode of tool, 0: short read; 1: long read, need for ChIA-PET data        |
+---------------------+--------------------------------------------------------------------------+
| --linker            | path of linker file, need for ChIA-PET mode                              |
+---------------------+--------------------------------------------------------------------------+
| --fastp             | fastp path, strong suggest for ChIA-PET data.                            |
+---------------------+--------------------------------------------------------------------------+
| --skipheader        | skip header N reads for detect linker, default 1000000.                  |
+---------------------+--------------------------------------------------------------------------+
| --linkerreads       | N reads used for detect linker, default 100000.                          |
+---------------------+--------------------------------------------------------------------------+
| --hichip            | Y(es) or N(o)[default] or O(nly print restriction site file without run  |
|                     | other step), need for hichip data                                        |
+---------------------+--------------------------------------------------------------------------+
| --ligation_site     | It can be the name of restriction enzyme, such as HindIII, MboI, DpnII,  |
|                     | Bglii, Sau3AI, Hinf1, NlaIII, AluI or the site of enzyme digestion,      |
|                     | A^AGCTT, ^GATC, ^GATC, A^GATCT, G^ANTC, CATG^, AG^CT or others.          |
|                     | multipe restriction enzyme can be seperated by comma, such as            |
|                     | G^ANTC,^GATC. restriction site with '^' and contains 'ATCG' without other|
|                     | character!!! if the genomic enzyme digestion file --restrictionsiteFile  |
|                     | is provided, this parameter does not need to be provided. only needed for|
|                     | hichip data                                                              |
+---------------------+--------------------------------------------------------------------------+
| --ResRomove         | Y or N, whether remove PET in same restriction contig. default: Y        |
+---------------------+-+------------------------------------------------------------------------+
| --restrictionsiteFile | restriction site file, can be genarated while has --ligation_site and  |
|                       | without this paramater or provide restriction enzyme information with  |
|                       | --ligation_site, we will automatically generate the file. only needed  |
|                       | for hichip data                                                        |
+---------------------+-+------------------------------------------------------------------------+
| --genomefile        | genome fasta file path, needed for with --ligation_site and without      |
|                     | --restrictionsiteFile only needed for hichip data                        |
+---------------------+-+------------------------------------------------------------------------+
| --minfragsizeMinimum  | restriction fragment length to consider, default 20                    |
+---------------------+-+------------------------------------------------------------------------+
| --maxfragsize       | Maximum restriction fragment length to consider, default 1000000         |
+---------------------+--------------------------------------------------------------------------+
| --minInsertsize     | Minimum restriction fragment skip of mapped reads to consider, default 1 |
+---------------------+--------------------------------------------------------------------------+			
| --fqmode            | single-end or paired-end (default), only required --fastq1 when          |
|                     | single-end mode for ChIA-PET data                                        |
+---------------------+------------+-------------------------------------------------------------+
| --minimum_linker_alignment_score | minimum alignment score, 14 default                         |
+---------------------+------------+-------------------------------------------------------------+
| --GENOME_INDEX      | the path of BWA index                                                    |
+---------------------+--------------------------------------------------------------------------+
| --GENOME_LENGTH     | the number of base pairs in the whole genome                             |
+---------------------+--------------------------------------------------------------------------+
| --CHROM_SIZE_INFO   | the file that contains the length of each chromosome, example file is in |
|                     | ChIA-PET_Tool_V3/chrInfo, this is necessary for > step 2 analysis.       |
|                     | Note. please make sure chromosome name in this file is same as name in   |
|                     | genome file!!!                                                           |
+---------------------+--------------------------------------------------------------------------+
| --CYTOBAND_DATA     | the ideogram data used to plot intra-chromosomal peaks and interactions, |
|                     | example file is in ChIA-PET_Tool_V3/chrInfo                              |
+---------------------+--------------------------------------------------------------------------+                    
| --SPECIES           | 1: human; 2: mouse; 3: others                                            |
+---------------------+--------------------------------------------------------------------------+
| Other options:                                                                                 |
+---------------------+--------------------------------------------------------------------------+
| --start_step        | start with which step, 1: linker filtering; 2: mapping to genome;        | 
|                     | 3: removing redundancy; 4: categorization of PETs; 5: peak calling;      |
|                     | 6: interaction calling; 7: visualizing, default: 1                       |
+---------------------+--------------------------------------------------------------------------+
| --stop_step         | stop with which step, 1: linker filtering; 2: mapping to genome;         |
|                     | 3: removing redundancy; 4: categorization of PETs; 5: peak calling;      |
|                     | 6: interaction calling; 7: visualizing, default: 100, should be bigger   |
|                     | than --start_step                                                        |
+---------------------+--------------------------------------------------------------------------+
| --output            | path of output, default: ChIA-PET_Tool_V3/output                         |
+---------------------+--------------------------------------------------------------------------+
| --prefix            | prefix of output files, default: out                                     |
+---------------------+--------------------------------------------------------------------------+
| --minimum_tag_length| minimum tag length, default: 18                                          |
+---------------------+--------------------------------------------------------------------------+
| --maximum_tag_length| maximum tag length, default: 1000                                        |
+---------------------+----+---------------------------------------------------------------------+
| --minSecondBestScoreDiff | the score difference between the best-aligned and the second-best   |
|                          | aligned linkers, default: 3                                         |
+---------------------+----+---------------+-----------------------------------------------------+
| --output_data_with_ambiguous_linker_info | whether to print the linker-ambiguity PETs,         |
|                                          | 0: not print; 1: print, default: 1                  |
+---------------------+--------------------+-----------------------------------------------------+
| --printreadID       | write read ID to bedpe file, default: N                                  |
+---------------------+--------------------------------------------------------------------------+
| --printallreads     | print all reads no matter strand, default: 0[print all]; 1, only print   |
|                     | valid strand reads.                                                      |
+---------------------+--------------------------------------------------------------------------+
| --search_all_linker | search all linkers in reads or just search one time, default: N          |
+-------------+-------+--------------------------------------------------------------------------+
| --thread    | the number of threads used in linker filtering and mapping to genome, default: 1 |
+-------------+-------+--------------------------------------------------------------------------+
| --MAPPING_CUTOFF    | cutoff of mapping quality score for filtering out low-quality or         |
|                     | multiply-mapped reads, default: 20                                       |
+---------------------+--------------------------------------------------------------------------+
| --MERGE_DISTANCE    | the distance limit to merge the PETs with similar mapping locations,     | 
|                     | default: 2                                                               |
+---------------------+-+------------------------------------------------------------------------+
| --SELF_LIGATION_CUFOFF| the distance threshold between self-ligation PETs and intra-chromosomal|
|                       |inter-ligation PETs, default: 8000 for ChIA, and 1000 for HiChIP        |
+---------------------+-+------------------------------------------------------------------------+
| --EXTENSION_LENGTH  | the extension length from the location of each tag, default: 500,        |
|                     | 1500 suggest for single-end mode                                         |
+---------------------+---+----------------------------------------------------------------------+
| --MIN_COVERAGE_FOR_PEAK | the minimum coverage to define peak regions, default: 5              |
+---------------------+---+----------------------------------------------------------------------+
| --PEAK_MODE         | 1: peak region mode, which takes all the overlapping PET regions above   |
|                     | the coverage threshold as peak regions; 2: peak summit mode, which takes |
|                     | the highest coverage of overlapping regions as peak regions, default: 2  |
+---------------------+-------+------------------------------------------------------------------+
| --MIN_DISTANCE_BETWEEN_PEAK | the minimum distance between two peaks, default: 500             |
+---------------------+-------+------------------------------------------------------------------+
| --GENOME_COVERAGE_RATIO     | the estimated proportion of the genome covered by the reads,     |
|                             | default: 0.8                                                     |
+---------------------+-------+------------------------------------------------------------------+
| --PVALUE_CUTOFF_PEAK        | p-value to filter peaks that are not statistically significant,  |
|                             | default: 0.00001                                                 |
+---------------------+-------+------------------------------------------------------------------+
| --INPUT_ANCHOR_FILE         | a file which contains user-specified anchors for interaction     |
|                             | calling, default: null                                           |
+---------------------+-------+------------------------------------------------------------------+
| --PVALUE_CUTOFF_INTERACTION | p-value to filter false positive interactions, default: 0.5      |
+-------------+-------+--------------------------------------------------------------------------+
| --zipbedpe  | gzip bedpe related file, after analysis done. default: N. Y for gzip, N for not. |
+-------------+-------+--------------------------------------------------------------------------+
| --zipsam    | Convert sam file to bam, after analysis done. default: N                         |
+-------------+-------+--------------------------------------------------------------------------+
| --deletesam | Delete sam files. default: N                                                     |
+-------------+-------+--------------------------------------------------------------------------+
| --keeptemp  | Keep temp sam and bedpe file. default: N                                         |
+-------------+-------+--------------------------------------------------------------------------+
| --map_ambiguous     | Also mapping ambiguous reads without linker. default: N                  |
+---------------------+--------------------------------------------------------------------------+
| --skipmap           | Skip mapping read1 and read2, start from paired R1.sam and R2.sam, only  |
|                     | valid in HiChIP mode now. default: N                                     |
+---------------------+--------------------------------------------------------------------------+
| --macs2             | macs2 path, using macs2 callpeak to detect anchor peak with alignment    | 
|                     | file. default: N                                                         |
+---------------------+--------------------------------------------------------------------------+
| --nomodel           | macs2 parameter, Whether or not to build the shifting model in macs2.    |
|                     | default: N                                                               |
+---------------------+--------------------------------------------------------------------------+
| --shortestP         | extend and keep shorest peak length longer than N for loop calling,      |
|                     | suggest 1500, user can set 0 to skip this step. default: 1500            |
+---------------------+--------------------------------------------------------------------------+
| --shortestA         | extend and keep shorest anchor length longer than N for loop calling,    |
|                     | user can set 0 to skip this step. default: 0                             |
+---------------------+--------------------------------------------------------------------------+
| --XOR_cluster       | Whether keep loops if only one side of anchor is overlap with peak.      |
|                     | default: N                                                               |
+---------------------+--------------------------------------------------------------------------+
| --addcluster        | Keep all regions with more than 2 count reads as potential anchor for    |
|                     | calling loop. default: N. if peaks number of macs2 smaller than 10000,   |
|                     | this paramater will work automaticly.                                    |
+---------------------+--------------------------------------------------------------------------+


Output files
^^^^^^^^^^^^

Output file format and details see "https://github.com/GuoliangLi-HZAU/ChIA-PET_Tool_V3#result-file".<br>

Output report details see "xxx" .<br>

.. tip:: For feature requests or bug reports please open an issue `on github <https://github.com/GuoliangLi-HZAU/ChIA-PET_Tool_V3>`__.
