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

### Introduction

The viral detection package was developed in Python and uses the BLAST tool for viral identification in RNA-seq data. A curated database and optimized parameters are used.

<a name="supported"></a>
### Supported files

The current version supports paired-end reads and unpaired reads. The files can be in two formats essentially:

- FASTQ or FASTQ.GZ:  

>@seq_ID  
>ATCTACTACTGACATAATAGCT  
>+  
>1****+*''))*E55CCF>>>>

- FASTA

> \>seq_ID  
>ACTGCTCGACGATGACTGCATG

### Pipeline


### Performance


| Data set | Disk space (GB) | Time (m) | Peak RAM usage (GB) | Additional disk space required (GB) |  
| :---: | :---: | :---: | :---: | :---: |
| May4.fastq | 4 | 120 | 8 | 4 |
| May4.fastq.gz | 2 | 110 | 8 | 4 |
| May4.fasta | 1.8 | 115 | 8 | 4 |


### Installation

The tool uses Python, BLAST, R project and RStudio to... 

### Prerequisites

**1. BLAST**

Please go to official [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download) page and install the correct version for you operative system. To verify that the tool works correctly, enter the command terminal and type: *blastn*

The installation was successful if you get the following message:

```markdown
BLAST query/options error: Either a BLAST database or subject sequence(s) must be specified
Please refer to the BLAST+ user manual.
```

**2. Python**

Please go to official [Python](https://www.python.org/downloads/) page and install the correct version (3.7+) for you operative system. To verify that the tool works correctly, enter the command terminal and type: *python --version*

The installation was successful if you get the following message:

```markdown
Python 3.7 (or superior)
```

**3. R project**

To download [R project](https://cran.r-project.org/mirrors.html) please choose your preferred CRAN mirror in the official page and the select the correct version for you operative system.

**4. RStudio**

It is necessary to have R project installed before this step. Please go to official [RStudio](https://rstudio.com/products/rstudio/download/) page and install the correct version for you operative system. To verify that the tool works correctly, run the program. 

Additional the following packages need to be installed

```markdown
- ggplot2
- RColorBrewer
- dplyr
- knitr
```

### Download

To properly use the identification tool it is necessary to download the following routines:

```markdown
-VirusDetectionPlatform_v1.py
-virusBLAST_v2.py
-non_redundant_sequences_v1.py
-identification_of_virus_species_V2.py
-identificacion_of_distant_viruses_V1.py
```

It is also necessary to download the databases:

```markdown
-PlantVirusesDB (.nhr, .nin, .nsq)
-FalsePositives (.nhr, .nin, .nsq)
```
The whole package can be downloaded in its compressed version [VDP project](https://github.com/MicrobialBiotechnologyLaboratory/Virus-Detection-Package/blob/master/vdp_project.zip). 
Individual scripts are also available in the repository.

### Tutorial

A paired RNA-seq data test set is available in the repository.




First open the command terminal and go to the folder where the downloaded files are located. The main script is called ***VirusDetectionPlatform_v1.py***. Copy the following line of text into the terminal:

```markdown
python3 VirusDetectionPlatform_v1.py test_file1.fastq test_file2.fastq
```
File1.fastq and file2.fastq correspond to the name of the files that will be analyzed. Then press enter and please be patient.

![GitHub Logo](/images/terminal_step1.png)

![GitHub Logo](/images/terminal_step2.png)

![GitHub Logo](/images/terminal_step3.png)

Results : 

![Viral Result](/images/vr1.png)

![Viral Result](/images/vr2.png)

![Viral Result](/images/vr3.png)

![Viral Result](/images/vr4.png)

![Viral Result](/images/vr5.png)

The average time for a paired file of four gigabytes (eight gigabytes in total) is two and a half hours.

### Support or Contact

Having troubles? Please contact us.
