# PVDP 1.0.1 Manual

* [General info](#Info)
* [Supported data](#Data)
* [Pipeline](#Pipeline)
* [Prerequisites](#Prerequisites)
* [Download](#Download)  
* [Execution](#Execution)
* [Optional arguments](#Examples)
* [Issues](#Issues)
* [Support or contact](#Support)

<a name="Info"></a>
## General info

<li>PVDP is an open source tool for the detection of plant viruses in RNAseq data designed to be used locally in desktop computers with moderate computational power. PVDP does not require data submission to third parties and can be run under LINUX, Windows or MacOS. </li>

<li>The pipeline requires a local installation of BLAST and Python3. Rstudio is optional but is required to process results into a user friendly hmtl report. </li>

<a name="Data"></a>
## Supported data

PVDP supports single- or paired-end data in either fasta or fastq format. Datasets can be compressed in gzip (.gz) format.


<a name="Pipeline"></a>
## Pipeline

The plant virus detection pipeline comprises four python scripts (*nonRedundantSequences.py*, *genomeBLAST.py*, *virusBLAST.py*, and *outputTables.py*)
that can be executed in a single step using the *PlantVirusDetection.py* script.

 ***nonRedundantSequences.py*** removes redundant sequences from the dataset and transforms it into a fasta file of non-redundant sequences ordered by abundance and labelled with a unique identifier that contains information on the rank and the number of counts in the original dataset.

Host sequences can be removed prior to the virus detection step using ***genomeBLAST.py***  against a custom databases for any plant host. This database must be supplied by the user. A BLAST database for the removal potato (*S. tuberosum* and *S. phureja*) sequences is included in the test files. 

***virusBLAST.py*** performs a search of putative viral sequences using a dc-megablast search against a curated and non-redundant database of plant viruses with a standardized title comprising information relevant to each virus. The plant virus database is included as part of the pipeline.

Crude results are processed using the ***outputTables.py*** script, which removes hits with low certainty. Plain results are saved in the *Tables* directory and ca be converted into a user friendly html report using ***virusReport.R*** script in Rstudio.

<img src="/assets/Fig1_200dpi.png" alt="drawing" width="500"/>

<a name="Prerequisites"></a>
## Prerequisites

Execution of the scripts requires a local installation of Python 3 (van Rossum and Drake 2009), Blast (Altschul et al. 1990) and Rstudio (R Core Team 2017; RStudio Team 2020). 


**BLAST+**

Please go to official [BLAST+](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download) page and install the correct version for you operative system. To verify that the tool works correctly, enter to the terminal or the command prompt and type: 

```sh
blastn
```

The installation was **successful** if you get the following message:

```markdown
BLAST query/options error : Either a BLAST database or subject sequence(s) must be specified. Please refer to the BLAST+ user manual.
```


**Python**

Please go to official [Python](https://www.python.org/downloads/) page and install the correct version (3.7+) for you operative system. To verify that the tool works correctly, enter to the terminal or the command prompt and type: 

```sh
python  --version
```

The installation was successful if you get a message like:

```markdown
Python 3 (or superior)
```

<ins>Important</ins>: *If you have a version lower than Python 3, the tool may not work correctly.*

If you get an **error** like:

```markdown
"python" is not recognized as an internal or external command, operable program or batch file.
```

Use the same command, but instead of **python** try **py**. A third option is to try **python3**. It is important to remember the option that worked for the later steps. If none of the previous solutions work, check the Issues section.


**RStudio**

Please go to official [RStudio](https://rstudio.com/products/rstudio/download/) page and install the correct version for you operative system (RStudio requires an existing installation of R).

Also the following packages need to be installed:

```markdown
- ggplot2
- RColorBrewer
- knitr
- rmarkdown
```

To verify that the tool works correctly, you can generate a HTML report from the test data available.


----


<a name="Download"></a>
## Download

You can obtain the detection package in its compressed version at the following <ins>[link](https://drive.google.com/drive/folders/1gk9KyMXeIE7wy1GjyiTgrEwD9sDhsASA?usp=sharing)</ins>. 

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

***The last update of the viral database was made on April, 2020.***


----


<a name="Execution"></a>
## Execution

Open the terminal or the command prompt and go to the folder where the downloaded files are located.

<ins>Help:</ins> If you want to know how to move between folders in the terminal or command prompt, check the following [link](https://biotecnologiamicrobianaunalmed.github.io/terminal-basics/).

To execute the program it is necessary to run the main script and give it the path of at least one fastq/fasta file. The main script is called ***plantVirusDetectionV2.py*** and it's located in the folder ***Scripts***. The general sctructure is: 

```markdown
python Scripts/plantVirusDetectionV2.py -seq1 <file_route> [options]
```

e.g. the following command is used to run the test data with the default options:

```markdown
python Scripts/plantVirusDetectionV2.py -seq1 Files/data.fastq
```

Then press enter and please be patient. The program displays messages in the terminal to inform about the step it is in. If everything works correctly you can see at the end the detected viruses in a summarized way. Also you can find the results in the *Files* folder.

The results folder includes eight tables in tsv (tab-separated values) format that summarize the running parameters, composition of the dataset, a curated table of results, and a summary of countries, host and references related to the viruses detected in the sample. These tables can be opened with standard spreadsheet programs or formatted as a user-friendly html report with Rstudio. 

<ins>Tip:</ins> When analyzing your own files it is recommended to put the files in the **Files** folder or directly in the pvdp folder, otherwise it is necessary to specify the full path of where they are located.


----


<a name="Examples"></a>
## PVDP examples

The program can receive multiple arguments, the most essential cases are described below:

* Single- reads:

    ```markdown
    python Scripts/plantVirusDetectionV2.py -seq1 <file_route>
    ```

* Paired-end reads:

    ```markdown
    python Scripts/plantVirusDetectionV2.py -seq1 <file_route> -seq2 <file2_route>
    ```

* Single- **or** paired-end reads, using a host database as a filter (currently only one database belonging to potato is available):

    ```markdown
    python Scripts/plantVirusDetectionV2.py -seq1 <file_route> -hostdb Potato_masked
    ```

    ```markdown
    It is not necessary to specify the path of Potato_masked, the program searches by default in the Databases folder.
    ```

* Single- **or** paired-end reads, using a specific amount of reads, e.g. 1000000. It is recommended to use this parameter when the data is very large and also to carry out an initial exploration of it (also to fix MemoryError in Step 1):

    ```markdown
    python Scripts/plantVirusDetectionV2.py -seq1 <file_route> -subset 1000000
    ```

* Single- **or** paired-end, using a specific amount of processors, e.g. 5 (the default quantity is 2):

    ```markdown
    python Scripts/plantVirusDetectionV2.py -seq1 <file_route> -num_threads 5
    ```

* More information about the arguments is available by executing the following command:

    ```markdown
    python Scripts/plantVirusDetectionV2.py --help
    ```

*Each argument is unique, but they can be combined at will.*


----


<a name="HTML report"></a>
## Generating user-friendly HTML report with RStudio

When the process ends it is possible to create the graphic report in html format. To do this you need to open the file **VirusReport.Rmd** in Rstudio and have the required packages installed. **VirusReport.Rmd** is located in the **Scripts** folder.

First modify the ***path_to_files*** variable directly in the script (line 14), specifying the full path to the Tables folder (1) found in the results folder that can be found in **Files/Results_data** (in the case of test data). Make sure that the path ends with a slash, otherwise you may get an error, i.e. **../Tables/**.

![Structure](/assets/rstudio1.png)

This step is crucial, if the correct path is not placed, the program will not run; the associated error is like:

```
Error in file(file, "rt") : unable to open connection
```

In the next step the script must be run from **Run All** (2).

![Structure](/assets/rstudio2.png)

When you use Run All (2) you should see a green loading bar at the bottom right like this:

![Structure](/assets/done.PNG)

The process ends once the bar loads completely. Then it is possible to **Knit** (3) the document and if everything was satisfactory a window will open with the respective report. If a window doesn't open, explore the Knit options (down arrow) and select "Knit to html".

![Structure](/assets/rstudio3.png)

You can close the window, the report is saved in the **Scripts** folder, under the name of *VirusReport.html*. It is recommended to change the file name or change folder, because if the script is executed with another data set it will be overwritten.


----


<a name="Issues"></a>
## Issues

* [python] **AND** [py] **AND** [python3] ... is not recognized as an internal or external command, operable program or batch file.**:

    ```markdown
    You may have Python installed through Anaconda(Windows systems), in this case you must open the Anaconda prompt. In other case Your version of Python is lower than the third. Please update it.
    ```

* MemoryError in Step 1:

    ```markdown
    You must use the -subset argument, because the available RAM memory cannot process the total size of the data. The recommended is three to five million sequences for common computer equipment.
    ```

* The program does not advance (hours) from step 1:

    ```markdown
    The data format is not supported.
    ```

* Username or folders:

    ```markdown
    Please do not use spaces in the names assigned to folders or even the username, the program will not work.
    ```

* ImportError: No moduled named statistics OR ValueError: math domain error

    ```markdown
    Your version of Python is lower than the third. Please update it.
    ```


----


<a name="Support"></a>
## Support or Contact

Having troubles? Please contact us. Address for communication is in license file.


