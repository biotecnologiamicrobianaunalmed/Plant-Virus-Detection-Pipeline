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

The following packages need to be installed:

```markdown
- ggplot2
- RColorBrewer
- knitr
```
<!---
To verify that the graphing section is working correctly download the consolidation of [result tables](https://github.com/biotecnologiamicrobianaunalmed/Plant-Virus-Detection-Package/blob/master/results_rna_physalis_peruviana.zip). Then open RStudio, configure the working directory correctly and specify the path in which the main file (***List_of_tables_rna_physalis_peruviana_1_rna_physalis_peruviana_2_nr.tsv***) is located.--->

<!---![Specify Path](/images/specify_path.png)--->

<!---Then run the program and view the generated file.---> 

<!---![Run All](/images/run_all.png)--->

<!---![Preview](/images/preview.png)--->

<!---This file can be opened in the browser and saved by pressing print.--->

<!---The generated report looks as follows:--->

<!---![Viral Result](/images/vr1.png)--->

<!---![Viral Result](/images/vr2.png)--->

<!---![Viral Result](/images/vr3.png)--->

<!---![Viral Result](/images/vr4.png)--->

<!---![Viral Result](/images/vr5.png)--->

<a name="Download"></a>
### Download

Before downloading the files make sure you meet the essential [prerequisites](#Prerequisites), i.e. **Python** and **BLAST**. If you want to generate a graphic report in html format, you must also meet the additional prerequisites.

You can obtain the detection package in its compressed version [here](https://drive.google.com/drive/folders/1gk9KyMXeIE7wy1GjyiTgrEwD9sDhsASA?usp=sharing). It contains the run and graph scripts, the databases and a test file.

Once the download is complete, locate the file in your preferred folder and unzip it; when you do this you will find the following structure:

```markdown
----->Scripts
       >hostFilterV2.py
       >nonRedundantSequencesV2.py
       >plantVirusDetectionV2.py
       >selectionOfPositives
       >virusBLASTV2.py
       >VirusReport.Rmd
       
----->Databases (18 files)
       >PlantVirusesDB_0420v4_masked.(naa, nab, nac, nhr, nin, nog, nsd, nsi, nsq).
       >Potato_masked.(naa, nab, nac, nhr, nin, nog, nsd, nsi, nsq).
       
----->Testfiles
       >data.fastq
```

Now you can continue with the next section.

***The last update of the viral database was made on April, 2020.***

<a name="Tutorial"></a>
### Tutorial

<!---!![Structure](/images/test_files.png)--->
Open the terminal or the command prompt and go to the folder where the downloaded files are located.

You can access the program's help by writing the following line:

```markdown
python Scripts/plantVirusDetectionV2.py --help
```
You must obtain the following information:

![Structure](/images/help.png)

If you get an error like:

```markdown
"python" is not recognized as an internal or external command, operable program or batch file.
```

Use the same command, but instead of **python** try **py**. A third option is to try **python3**. If none of the previous solutions work, check the troubleshooting section.

To execute the program it is necessary to run the main script and give it the path of at least one fastq file. The main script is called ***plantVirusDetectionV2.py*** and it's located in the folder ***Scripts***. The structure of the command is as follows:

```markdown
python Scripts/plantVirusDetectionV2.py -seq1 Testfiles/data.fastq
```

Then press enter and please be patient. 

The program displays messages in the terminal to inform about the step it is in, at the end you can see the viruses detected in a summarized way. 

You can find the results in the *Testfiles* folder, and there will be the *Results_data* folder that should look like this:

![Structure](/images/result_folder.PNG)

With the previous results you can continue with the graphing section.

You can also use a database as a filter, this will make the process more efficient if the host of the sample is potato. The command would be like this:

```markdown
python Scripts/plantVirusDetectionV2.py -seq1 Testfiles/data.fastq -hostdb Potato_masked 
```

**GRAPHING**

When the process ends it is possible to create the graphic report in html format. To do this you need to open the file **VirusReport.Rmd** in Rstudio and have the required packages installed. 

First modify the *path_to_files* variable, specifying the full path to the Tables folder (1) found in the results folder, Run All (2) and Knit the document (3).

![Structure](/images/rstudio.PNG)

Make sure that the path (1) ends with a slash, otherwise you may get an error, i.e. **../Tables/**.

When you use Run All (2) you should see a green loading bar at the bottom right like this:

![Structure](/images/done.PNG)

The process ends once the bar loads completely. Then it is possible to Knit (3) the document and if everything was satisfactory a window will open with the respective report.

You can close the window, the report is saved in the **Scripts** folder, under the name of *VirusReport.html*.


**TROUBLESHOOTING**

- Windows systems:

> python **AND** py **AND** python3 ... is not recognized as an internal or external command, operable program or batch file.

You may have python installed through Anaconda, in this case you must open the Anaconda prompt.

<a name="Support"></a>
### Support or Contact

Having troubles? Please contact us.
