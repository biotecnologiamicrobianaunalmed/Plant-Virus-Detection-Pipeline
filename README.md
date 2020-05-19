# PVDP 1.0.1 Manual

1. [Introduction](#Introduction)  
   1.1. [Supported files](#supported)  
   1.2. [Pipeline](#Pipeline)  
   1.3. [Performance](#Performance)
   
2. [Installation](#Installation)  
   2.1. [Prerequisites](#Prerequisites)   
   2.2. [Download](#Download)
  
3. [Tutorial](#Tutorial)  

4. [Support or contact](#Support)

<a name="Introduction"></a>
### Introduction

*...Developing...*

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

*Out of date graphic*

<a name="Performance"></a>
### Performance

The test data (*data.fastq [1e+06 reads]*) was tested on the following computer equipment:

| Operating system | Processor| RAM | Total execution time (s) |  
| :---: | :---: | :---: | :---: |
| Windows 7 64-bit | Intel Core i5-2300 CPU @ 2,8 GHz | 8 GB | 509 |
| Windows 10 64-bit | Intel Core i5-6200 CPU @ 2,3 GHz | 4 GB | 954 |
| Ubuntu 18.04.4 LTS | Intel core i3-7100 CPU @ 2,4 GHz | 4 GB | 590 |
| Windows 10 64-bit | Intel core i3-4005 CPU @ 1.7 GHz | 4 GB | 1990 |
| Ubuntu 18.04.4 LTS | Intel Core i5-2300 CPU @ 2,8 GHz | 8 GB | 432 |

Additionally, a data set was evaluated modifying the sequence length, the total execution time were monitored. The results are summarized below:

![Structure](/images/timeVlength.png)

This test was carried out on the following computer equipment, Windows 7 64-bit / Intel Core i5-2300 CPU @ 2,8 GHz / 8 GB RAM. 

----

<a name="Installation"></a>
### Installation

Sequence alignment is done through BLAST, the algorithms for automatic execution and filtering are written in Python. It is possible to interpret the result tables to generate a graphic report using Rproject and RStudio.

<a name="Prerequisites"></a>
### Prerequisites

**1. BLAST+**

Please go to official [BLAST+](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download) page and install the correct version for you operative system. To verify that the tool works correctly, enter to the terminal or the command prompt and type: 

```sh
blastn
```

The installation was **successful** if you get the following message:

```markdown
BLAST query/options error : Either a BLAST database or subject sequence(s) must be specified
Please refer to the BLAST+ user manual.
```

**2. Python**

Please go to official [Python](https://www.python.org/downloads/) page and install the correct version (3.7+) for you operative system. To verify that the tool works correctly, enter to the terminal or the command prompt and type: 

```sh
python  --version
```

The installation was successful if you get a message like:

```markdown
Python 3.7 (or superior)
```

<ins>Important</ins>: *If you have a version lower than Python 3, the tool may not work correctly.*

If you get an **error** like:

```markdown
"python" is not recognized as an internal or external command, operable program or batch file.
```

Use the same command, but instead of **python** try **py**. A third option is to try **python3**. If none of the previous solutions work, check the Issues section.

**3. R project**

To download [R project](https://cran.r-project.org/mirrors.html) please choose your preferred CRAN mirror in the official page and then select the correct version for you operative system.

**4. RStudio**

It is necessary to have R project installed before this step. Please go to official [RStudio](https://rstudio.com/products/rstudio/download/) page and install the correct version for you operative system. To verify that the tool works correctly, run the program. 

The following packages need to be installed:

```markdown
- ggplot2
- RColorBrewer
- knitr
- rmarkdown
```

----
<a name="Download"></a>
### Download

Before downloading the files make sure you meet the essential [prerequisites](#Prerequisites), i.e. **Python** and **BLAST**. If you want to generate a graphic report in html format, you must also meet the additional prerequisites.

You can obtain the detection package in its compressed version at the following [link](https://drive.google.com/drive/folders/1gk9KyMXeIE7wy1GjyiTgrEwD9sDhsASA?usp=sharing). It contains the run and graph scripts, the databases and a test file.

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
       
----->Files
       >data.fastq
```

Now you can continue with the next section.

***The last update of the viral database was made on April, 2020.***

----

<a name="Tutorial"></a>
### Tutorial

<!---!![Structure](/images/test_files.png)--->
Open the terminal or the command prompt and go to the folder where the downloaded files are located.

<ins>Help:</ins> If you want to know how to move between folders in the terminal or command prompt, check the following [link](https://github.com/biotecnologiamicrobianaunalmed/terminal-basics).

You can access the program's help by writing the following line:

```markdown
python Scripts/plantVirusDetectionV2.py --help
```
You must obtain the following information:

![Structure](/images/help.png)

If you get an **error** like:

```markdown
"python" is not recognized as an internal or external command, operable program or batch file.
```

Use the same command, but instead of **python** try **py**. A third option is to try **python3**. If none of the previous solutions work, check the Issues section.

**Execution**

To execute the program it is necessary to run the main script and give it the path of at least one fastq file. The main script is called ***plantVirusDetectionV2.py*** and it's located in the folder ***Scripts***. 

The following command is used to run the test data that comes with the program.

```markdown
python Scripts/plantVirusDetectionV2.py -seq1 Files/data.fastq
```

Then press enter and please be patient. The program displays messages in the terminal to inform about the step it is in; it is running correctly if you see something like:

![Structure](/images/start.PNG)

It is possible that an insufficient RAM memory error occurs, the program stops and at the end of step 1 "MemoryError" is observed, in this case it is necessary to use the -subset argument (see case 4). The recommended is three to five million sequences for common computer equipment. To see the most common errors, check the **Issues** section at the end.


If everything works correctly you can see at the end the detected viruses in a summarized way like:

![Structure](/images/end.PNG)

You can find the results in the *Files* folder, and there will be the *Results_data* folder that should look like this:

![Structure](/images/result_folder.PNG)

With the previous results you can continue with the graphing section.

<ins>Hint:</ins> When analyzing your own files it is recommended to put the files in the Files folder or directly in the pvdp folder, otherwise it is necessary to specify the full path of where they are located.

**Additional information**

The current version of PVDP works with mate-pairs and unpaired reads from Illumina sequencing technology (FASTQ.GZ, FASTQ or FASTA formats are supported). The program can receive multiple arguments, the most essential cases are described below:

*<ins>Case 1</ins>: Unpaired reads.*

>python Scripts/plantVirusDetectionV2.py -seq1 Path/to/file

*<ins>Case 2</ins>: Mate-pairs reads.*

>python Scripts/plantVirusDetectionV2.py -seq1 Path/to/file -seq2 Path/to/file/mate

*<ins>Case 3</ins>: Mate-pairs **or** unpaired reads, using a host database as a filter. Currently only one database belonging to potato is available. This allows the process to be more efficient.*

>python Scripts/plantVirusDetectionV2.py -seq1 Path/to/file -hostdb Potato_masked

>It is not necessary to specify the path of Potato_masked, the program searches by default in the Databases folder. It is also possible to use a specific database by entering the appropriate files in the aforementioned folder.

*<ins>Case 4</ins>: Mate-pairs **or** unpaired reads, using a specific amount of reads, e.g. 1000000. It is recommended to use this parameter when the data is very large and also to carry out an initial exploration of it.*

>python Scripts/plantVirusDetectionV2.py -seq1 Path/to/file -subset 1000000

*<ins>Case 5</ins>: Mate-pairs **or** unpaired reads, using a specific amount of processors, e.g. 5. The default quantity is 2.*

>python Scripts/plantVirusDetectionV2.py -seq1 Path/to/file -num_threads 5

More information about the arguments is available by executing the following command:

>python Scripts/plantVirusDetectionV2.py --help

*Each argument is unique, there is no need to repeat it when analyzing mated paires reads.*

**Graphing**

When the process ends it is possible to create the graphic report in html format. To do this you need to open the file **VirusReport.Rmd** in Rstudio and have the required packages installed. **VirusReport.Rmd** is located in the **Scripts** folder.

First modify the ***path_to_files*** variable directly in the script (line 14), specifying the full path to the Tables folder (1) found in the results folder that can be found in **Files/Results_data**. Make sure that the path ends with a slash, otherwise you may get an error, i.e. **../Tables/**.

![Structure](/images/rstudio1.png)

This step is crucial, if the correct path is not placed, the program will not run; the associated error is like:

```
Error in file(file, "rt") : unable to open connection
```

In the next step the script must be run from **Run All** (2).

![Structure](/images/rstudio2.png)

When you use Run All (2) you should see a green loading bar at the bottom right like this:

![Structure](/images/done.PNG)

The process ends once the bar loads completely. Then it is possible to **Knit** (3) the document and if everything was satisfactory a window will open with the respective report. If a window doesn't open, explore the Knit options (down arrow) and select "Knit to html".

![Structure](/images/rstudio3.png)

You can close the window, the report is saved in the **Scripts** folder, under the name of *VirusReport.html*. It is recommended to change the file name or change folder, because if the script is executed with another data set it will be overwritten.

----

**Issues**

- **Windows systems**:

> python **AND** py **AND** python3 ... is not recognized as an internal or external command, operable program or batch file.

You may have python installed through Anaconda, in this case you must open the Anaconda prompt.

- **MemoryError in Step 1**

> You must use the -subset argument, because the available ram memory cannot process the total size of the data.

- **The program does not advance from step 1**

> Please check that the format of the [supported files](#supported) is correct. The fastq format may not be in the specified format.

- **Username or folders**

> Please do not use spaces in the names assigned to folders or even the username, the program will not work.

- **ImportError: No moduled named statistics OR ValueError: math domain error**

> Your version of python is lower than the third. Please update it.

<a name="Support"></a>
### Support or Contact

Having troubles? Please contact us.
