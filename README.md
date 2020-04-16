# PVDP 1.0 Manual

1. [Introduction](#Introduction)  
   1.1. [Supported files](#supported)  
   1.2. [Pipeline](#Pipeline)  
   1.3. [Performance](#Performance)
   
2. [Installation](#Installation)  
   2.1. [Prerequisites](#Prerequisites)   
   2.2. [Downloading project](#Download)
  
3. [Tutorial](#Tutorial)  

4. [Support or contact](#Support)

<a name="Introduction"></a>
### Introduction

The low yields of many crops around the world are explained, among other aspects, by the lack of good phytosanitary management practices in addition to the widespread use of planting material not certified for its viral health. The use of next generation sequencing (NGS) has allowed the complete or partial characterization of a significant number of viral variants that infect crops in different regions of the world.

This tool was carried out in order to strengthen the programs of genetic improvement, quarantine surveillance and certification of planting material. This package is free to use and is specific for the diagnosis of viruses in plants. 

<a name="supported"></a>
### Supported files

The current version supports paired-end reads and unpaired reads, products of massively parallel sequencing technology [NGS](https://www.illumina.com/science/technology/next-generation-sequencing.html). The files can be in two formats essentially:

- FASTQ or FASTQ.GZ:  

>@seq_ID                              [1]
>
>CTCAGCTAAATACTTTGACACCNGTANNANNNN    [2]
> 
> \+                                  [3]
>
>BBDEBDDDDHHHHFHEEEEEEEE#3AC#####   [4]

FASTQ file is composed of four lines. [1] This line includes a unique ID and information such as flow cell lane information. [2] This line includes the nucleotides of the sequence. [3] A separator item (+). [4] This line includes quality values about sequences; this quality is denominated Phred Score and is described in ASCII symbols, every simbol has a respective number asociated and a higher number signifies higher acurracy of each nucleotide.

- FASTA

> \>seq_ID                            [1]
>
>ACTGCTCGACGATGACTGCATGCTGCACTGTCA    [2]

FASTA file is composed of two lines. [1] This line includes a unique ID. [2] This line includes the nucleotides of the sequence.

<a name="Pipeline"></a>
### Pipeline

![Pipeline](/images/pvdp_pipeline.png)

<a name="Performance"></a>
### Performance

The following results were obtained by performing the analysis on an Intel Core i5 9500 CPU @ 3.00 GHz * 6, 16 GB RAM, using the package of Python [Memory Profiler](https://pypi.org/project/memory-profiler/).

| Data set | Disk space (MB) | Time (m) | Peak RAM usage (GB) | Additional disk space required (MB) |  
| :---: | :---: | :---: | :---: | :---: |
| rna_physalis_peruviana.fastq (paired) | 54 | 5.8 | 2.62 | 17.6 |

![Memory Profile](/images/memory_profile_physalis.png)


| Data set | Disk space (MB) | Time (m) | Peak RAM usage (GB) | Additional disk space required (MB) |  
| :---: | :---: | :---: | :---: | :---: |
| rna_solanum_phureja.fastq.gz | 1848 | 144 | 2 | 473.3 |

![Memory Profile](/images/memory_profile_phureja.png)

Additionally, the execution time and the maximum peak of ram were evaluated for a set of NGS data obtained from leaf tissue of physalis peruviana. Seven data sizes were evaluated, each interval was one million reads. The following graphs summarize the information obtained:

![Memory Profile](/images/time_physalis.png)

![Memory Profile](/images/peak_physalis.png)


<a name="Installation"></a>
### Installation

Sequence alignment is done through BLAST, the algorithms for automatic execution and filtering are written in Python. It is possible to interpret the result tables to generate a graphic report using Rproject and RStudio.

<a name="Prerequisites"></a>
### Prerequisites

**1. BLAST**

Please go to official [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download) page and install the correct version for you operative system. To verify that the tool works correctly, enter the command terminal and type: *blastn*

The installation was successful if you get the following message:

```markdown
BLAST query/options error : Either a BLAST database or subject sequence(s) must be specified
Please refer to the BLAST+ user manual.
```

**2. Python**

Please go to official [Python](https://www.python.org/downloads/) page and install the correct version (3.7+) for you operative system. To verify that the tool works correctly, enter the command terminal and type: *python --version*

The installation was successful if you get the following message:

```markdown
Python 3.7 (or superior)
```

**3. R project**

To download [R project](https://cran.r-project.org/mirrors.html) please choose your preferred CRAN mirror in the official page and then select the correct version for you operative system.

**4. RStudio**

It is necessary to have R project installed before this step. Please go to official [RStudio](https://rstudio.com/products/rstudio/download/) page and install the correct version for you operative system. To verify that the tool works correctly, run the program. 

Additional the following packages need to be installed

```markdown
- ggplot2
- RColorBrewer
- dplyr
- knitr
- rworldmap
```
To verify that the graphing section is working correctly download the consolidation of [result tables](https://github.com/biotecnologiamicrobianaunalmed/Plant-Virus-Detection-Package/blob/master/results_rna_physalis_peruviana.zip). Then open RStudio, configure the working directory correctly and specify the path in which the main file (***List_of_tables_rna_physalis_peruviana_1_rna_physalis_peruviana_2_nr.tsv***) is located.

![Specify Path](/images/specify_path.png)

Then run the program and view the generated file. 

![Run All](/images/run_all.png)

![Preview](/images/preview.png)

This file can be opened in the browser and saved by pressing print.

The generated report looks as follows:

![Viral Result](/images/vr1.png)

![Viral Result](/images/vr2.png)

![Viral Result](/images/vr3.png)

![Viral Result](/images/vr4.png)

![Viral Result](/images/vr5.png)

<a name="Download"></a>
### Download

Before downloading the files make sure python works correctly verifying the version from the terminal. There are two options:

```markdown
python --version
```
If this command works, download [Scripts_python.zip](https://github.com/biotecnologiamicrobianaunalmed/Plant-Virus-Detection-Package/tree/master/package_scripts/Scripts_python.zip).

```markdown
python3 --version
```
If this command works, download [Scripts_python3.zip](https://github.com/biotecnologiamicrobianaunalmed/Plant-Virus-Detection-Package/tree/master/package_scripts/Scripts_python3.zip).

If none of the above options work, you may have python installed through Anaconda, in this case you must open the Anaconda prompt and check the previous commands.

Once the download is complete, locate the file in your preferred folder and unzip it; when you do this you will find the following structure:

```markdown
----->Scripts
       >hostFilter_prueba.py
       >nonRedundantSequences_prueba.py
       >outputTables_prueba.py 
       >plantVirusDetection_prueba.py
       >virusFilter_prueba.py      
```

The next step is to download the corresponding files to the [database](https://drive.google.com/drive/folders/1eZGH2zKl27UN87QtIdgRrzEC-UR7zuoP?usp=sharing). Once downloaded they should be placed in a folder called ***Databases***, next to the ***Scripts*** folder. Once the files are downloaded you will see something like this:

```markdown
----->Databases
       >maskedPlantVirusDBv2.(naa, nab, nac, nhr, nin, nog, nsd, nsi, nsq), that is, nine files.
       >Potato_masked.(naa, nab, nac, nhr, nin, nog, nsd, nsi, nsq), that is, nine files.
  ```

Now you can continue with the next section.

***The last update of the viral database was made on October 25, 2019.***

<a name="Tutorial"></a>
### Tutorial

To verify the integrity and operation of the package, download Illumina sequencing [test files](https://drive.google.com/drive/folders/1ECg3ibd5U9mzOif9MGeNvkAq1tKTcdij?usp=sharing) (one is enough). Create an additional folder (you can use any name) next to the two previously created and locate the downloaded file there, the ideal is to have something like this:

![Structure](/images/test_files.png)

Open the command terminal and go to the folder where the downloaded files are located. The main script is called ***plantVirusDetection_prueba.py*** and it's located in the folder ***Scripts***. 

To run the program it is necessary to run the main script with python and give it the path of the fastq files, the structure is as follows:

```markdown
python3 Scripts/plantVirusDetection_prueba.py -seq1 Test_files/Dic1_1a.fastq -hostdb Potato_masked 
```

Then press enter and please be patient. The program displays messages in the terminal to inform about the step it is in.

For additional information about the main script, run the following command:

```markdown
python3 Scripts/plantVirusDetection_prueba.py --help
```
You must obtain the following information:

```markdown
usage: identifyPlantVirusesV2.py [-h] -seq1 SEQ1 [-seq2 SEQ2] [-hostdb HOSTDB]
                                 [-num_threads NUM_THREADS] [-append] [-o O]
                                 [-subset SUBSET] [-ra] [-top TOP]
                                 [-threshold THRESHOLD] [-filtering_db]

optional arguments:
  -h, --help            show this help message and exit
  -seq1 SEQ1            path to sequence file 1 in fastq or fasta format
  -seq2 SEQ2            path to sequence file 2 in fastq or fasta format
  -hostdb HOSTDB        path to custom filtering DB or default DBs: Potato,
                        Gulupa or CapeGooseberry
  -num_threads NUM_THREADS
                        number of processors to use during BLAST searches
  -append               create filtered sequence files progressively. Slow but
                        requires less RAM
  -o O                  basename of output directory and files
  -subset SUBSET        use the specified number of reads for analysis
  -ra                   do not include reads with ambiguous base calls
  -top TOP              use only the most abundant non redundant reads for
                        analysis
  -threshold THRESHOLD  exclude non redundant reads below the specified
                        sequence count
  -filtering_db         uses custom filtering_db
```

<a name="Support"></a>
### Support or Contact

Having troubles? Please contact us.
