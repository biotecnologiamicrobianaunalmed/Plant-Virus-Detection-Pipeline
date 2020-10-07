# PVDP 1.0.1 Manual

* [General info](#Info)
* [Supported data](#Data)
* [Pipeline](#Pipeline)
* [Prerequisites](#Prerequisites)
* [Installation](#Installation)  
* [Examples](#Examples)
* [Available parameters](#Parameters)
* [Known issues](#Issues)
* [Support](#Support)
* [Citation](#Citation)
<a name="Info"></a>
## General info

<li>PVDP is an open source tool for the detection of plant viruses in RNAseq data designed to be used locally in desktop computers with moderate computational power. PVDP does not require data submission to third parties and can be run under LINUX, Windows or MacOS. </li>

<li>The pipeline requires a local installation of BLAST and Python3. Rstudio is optional but is required to process results into a user friendly hmtl report.</li>

<li>PVDP scripts and test files can be downloaded at this link: 
     https://drive.google.com/drive/folders/1_sSTEjxtYMMA_Sc5TJo3LOMfuBjHZA2t?usp=sharing  
       
</li> 
       
<a name="Data"></a>
## Supported data

PVDP supports single- or paired-end data in either fasta or fastq format. Datasets can be compressed in gzip (.gz) format.


<a name="Pipeline"></a>
## Pipeline

The plant virus detection pipeline comprises four python scripts (*nonRedundantSequences.py*, *genomeBLAST.py*, *virusBLAST.py*, and *outputTables.py*)
that can be executed in a single step using the *PVDP.py* script.

 ***nonRedundantSequences.py*** removes redundant sequences from the dataset and transforms it into a fasta file of non-redundant sequences ordered by abundance and labelled with a unique identifier that contains information on the rank and the number of counts in the original dataset.

Host sequences can be removed prior to the virus detection step using ***genomeBLAST.py***  against a custom databases for any plant host. This database must be supplied by the user. A BLAST database for the removal potato (*S. tuberosum* and *S. phureja*) sequences is included in the test files. 

***virusBLAST.py*** performs a search of putative viral sequences using a dc-megablast search against a curated and non-redundant database of plant viruses with a standardized title comprising information relevant to each virus. The plant virus database is included as part of the pipeline.

Crude results are processed using the ***outputTables.py*** script, which removes hits with low certainty. Plain results are saved in the *Tables* directory and can be converted into a user friendly html report using ***virusReport.R*** script in Rstudio.

<img src="/assets/Fig1_400dpi.png" alt="drawing" width="600"/>

<a name="Prerequisites"></a>
## Prerequisites
**BLAST**

Please go to the official [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download) page and install. Installation instructions can be found [here](https://www.ncbi.nlm.nih.gov/books/NBK279671/).


**Python**

Please go to the official [Python](https://www.python.org/downloads/)
page and install the right version (3.7+) for you operating system. To verify that python was installed properly, open the terminal and type: 

```sh
python  --version
```

The installation was successful if you get a message like this:

```markdown
Python 3.x.x
```

<ins>Important</ins>: *PVDP may not not correctly under earlier python releases.*

If you get an **error** like this:

```markdown
"python" is not recognized as an internal or external command, operable program or batch file.
```

Try **py** or **python3** instead. It is important to remember the option that worked for you as this will be used to launch PVDP. If none of the previous solutions work, check the issues section.


**RStudio**

Please go to the official [RStudio](https://rstudio.com/products/rstudio/download/) page and install the correct version for you operating system (RStudio requires an installation of R). The following packages are required:

* ggplot2
* RColorBrewer
* knitr
* rmarkdown

Detailed instructions on how to Install R, RStudio and R Packages can be found [here](https://data-flair.training/blogs/how-to-install-r/)

<a name="Installation"></a>
## PVDP Installation

PVDP scripts and test files can be downloaded [here](https://drive.google.com/drive/folders/1_sSTEjxtYMMA_Sc5TJo3LOMfuBjHZA2t?usp=sharing). Just download the files and place them where you find it convenient. Files should have the following folder structure:

<img src="/assets/FileStructure.gif"/>


<a name="Examples"></a>

## Examples

### Executing PVDP with default parameters using a single dataset
To analize a single dataset without using a host filter database type the following from the PVDP folder:

```markdown
python3 PVDP/Scripts/PVDP.py -seq1 <file location> 
```
To run the dataset testData_SPhureja_1.fastq.gz, move to the PVDP_dir and type the following:
```markdown
python3 PVDP/Scripts/PVDP.py -seq1 Datasets/testData_SPhureja_1.fastq.gz 
```
When run correctly, you will find a file within the Datasets folder contaning a summary of results in a newly created folder with the name Results_testData_SPhureja_1
During execution you should an output similar to this:

```markdown

==========================================
       Plant Virus Detection Program
==========================================
Parameters
Sequence file 1:	 Datasets/testData_SPhureja_1.fastq.gz
Sequence file 2:	 None
Host dababase:		 None
Number of processors:	 2
Output folder:		 None
Subset size:		 None
Remove bad reads:	 False
Top nr sequences:	 None
Abundance threshold:	 None

==========================================
 Step 1: Removal of redundant sequences
==========================================
Verifying file testData_SPhureja_1.fastq.gz
gz is an accepted file extension
Processing file:  testData_SPhureja_1.fastq

Total sequences:	 1000000
Non-redundant sequences: 417828
Redundancy:		 58.2%

Execution time of step 1: 25.619 seconds

==========================================
 Step 2: Host filter
==========================================
Filtering step was not chosen.
Continuing with virus detection step.

Execution time of step 2: 0.011 seconds

==========================================
 Step 3: Virus Detection
==========================================
Running testData_SPhureja_1_nr.fa  against  PlantVirusesDB_0420v4_masked

Execution time of step 3: 473.208 seconds

==========================================
                 Results
==========================================
Detected viruses:

Potato_virus_X (Potexvirus/Alphaflexiviridae) :
  Reads per million:		6389.0 
  Counts:			6389 
  Median E-value:		2.6e-43 
  Average percent identity:	98.2 
  Eveness:			0.97 
  Residuals(stdv):		6.74 
  Probability:			100.0

Potato_virus_S (Carlavirus/Betaflexiviridae) :
  Reads per million:		4249.0 
  Counts:			4249 
  Median E-value:		2.2e-44 
  Average percent identity:	98.9 
  Eveness:			0.9 
  Residuals(stdv):		17.4 
  Probability:			99.9

Potato_virus_V (Potyvirus/Potyviridae) :
  Reads per million:		2095.0 
  Counts:			2095 
  Median E-value:		5.1e-46 
  Average percent identity:	97.9 
  Eveness:			0.96 
  Residuals(stdv):		5.16 
  Probability:			100.0

Potato_yellow_vein_virus(RNA2) (Crinivirus/Closteroviridae) :
  Reads per million:		77.0 
  Counts:			77 
  Median E-value:		5.1e-46 
  Average percent identity:	99.5 
  Eveness:			0.81 
  Residuals(stdv):		5.8 
  Probability:			99.9

Potato_yellow_vein_virus(RNA3) (Crinivirus/Closteroviridae) :
  Reads per million:		65.0 
  Counts:			65 
  Median E-value:		5.1e-46 
  Average percent identity:	99.5 
  Eveness:			0.79 
  Residuals(stdv):		10.24 
  Probability:			99.8

Potato_virus_Y (Potyvirus/Potyviridae) :
  Reads per million:		61.0 
  Counts:			61 
  Median E-value:		5.1e-46 
  Average percent identity:	99.4 
  Eveness:			0.77 
  Residuals(stdv):		7.07 
  Probability:			99.8

Potato_mop-top_virus(RNA2) (Pomovirus/Virgaviridae) :
  Reads per million:		38.0 
  Counts:			38 
  Median E-value:		5.1e-46 
  Average percent identity:	99.6 
  Eveness:			0.69 
  Residuals(stdv):		9.75 
  Probability:			99.2

putative_Tobamovirus (Tobamovirus/Virgaviridae) :
  Reads per million:		30.0 
  Counts:			30 
  Median E-value:		2.5e-18 
  Average percent identity:	85.8 
  Eveness:			0.65 
  Residuals(stdv):		10.69 
  Probability:			98.5

Potato_mop-top_virus(RNA1) (Pomovirus/Virgaviridae) :
  Reads per million:		28.0 
  Counts:			28 
  Median E-value:		1.1e-45 
  Average percent identity:	99.6 
  Eveness:			0.69 
  Residuals(stdv):		21.09 
  Probability:			98.1

Potato_yellow_vein_virus(RNA1) (Crinivirus/Closteroviridae) :
  Reads per million:		21.0 
  Counts:			21 
  Median E-value:		2.2e-44 
  Average percent identity:	98.3 
  Eveness:			0.57 
  Residuals(stdv):		16.14 
  Probability:			92.9

Potato_mop-top_virus(RNA3) (Pomovirus/Virgaviridae) :
  Reads per million:		18.0 
  Counts:			18 
  Median E-value:		5.1e-46 
  Average percent identity:	99.8 
  Eveness:			0.55 
  Residuals(stdv):		28.8 
  Probability:			77.5

putative_Solendovirus (Solendovirus/Caulimoviridae) :
  Reads per million:		12.0 
  Counts:			12 
  Median E-value:		1.5e-17 
  Average percent identity:	83.3 
  Eveness:			0.46 
  Residuals(stdv):		9.34 
  Probability:			82.2

Total execution time: 498.854 seconds
```

### Executing PVDP with default parameters using paired-end data
For paired-end data, just add the mate dataset set using the parameter -seq2 as shown in the example below:

```markdown
python3 PVDP/Scripts/PVDP.py -seq1 <file location> -seq2 <file location> 
```
For example, to analyze the datasets testData_SPhureja_1.fastq.gz and testData_SPhureja_2.fastq.gz, type:

```markdown
python3 PVDP/Scripts/PVDP.py -seq1 Datasets/testData_SPhureja_1.fastq.gz -seq2 Datasets/testData_SPhureja_2.fastq.gz
```

### Executing PVDP with a host sequence filter
Execution times can significantly improve if a BLAST database of the target host is available. This also removes endogenous viral-like sequences from the analysis. For Potato, a custom database is included in Database folder (Potato_masked). To use a host filtering database just add the -hostdb parameter followed by the location of the database, like this:

```markdown
python3 PVDP/Scripts/PVDP.py -seq1 <file location> -seq2 <file location> -hostdb <database location> 
```
To run the test files, type:

```markdown
python3 PVDP/Scripts/PVDP.py -seq1 Datasets/testData_SPhureja_1.fastq.gz -seq2 Datasets/testData_SPhureja_2.fastq.gz -hostdb PVDP/Databases/Potato_masked
```

### Executing PVDP on a data subset
For exploratory analysis of data or execution on low-performance computers, a subset of sequences can be anlyzed using the -subset parameter. This parameter avoids a complete analysis of large dataset, is faster, and requires less memory.

to analyze a subset of 10000 sequences in a paired-end  dataset, type:

```markdown
python3 PVDP/Scripts/PVDP.py -seq1 <file location> -seq2 <file location> -hostdb <database location> -subset 10000
```
To run the test files, type:
```markdown
python3 PVDP/Scripts/PVDP.py -seq1 Datasets/testData_SPhureja_1.fastq.gz -seq2 Datasets/testData_SPhureja_2.fastq.gz -hostdb PVDP/Databases/Potato_masked -subset 10000
```

<a name="Parameters"></a>

## Available parameters

The following table illustrates the parameters currently available for the execution of PVDP. They can be implemente using the following syntax.

```markdown
python Scripts/PVDP.py -seq1 <file_route> [options]
```
| Parameter       | Description     | Type     |
| :------------- | :---------- | :----------- |
|  -seq1(required) | Path to sequence file 1   | String    |
|  -seq2 | Path to sequence file 2   | String    |
|  -hostdb| Path to BLAST database of host sequences   | String    |
|  -num_threads| Number of processors to be used   | Integer    |
|  -subset| Analyzes a subset of reads of the specified size   | Integer    |
|  -remove_bad_reads| Removes reads with ambiguous base calls    | Boolean    |
|  -top| Analyzes the most abundant non-redundant sequences    | Integer    |
|  -threshold| Removes non-redundant reads with low abundance   | Integer    |





### Generation of the HTML report 

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
## Known issues

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


<a name="Support"></a>
## Support

Having troubles? Please contact us at: lab labmicrobiologia_med@unal.edu.co. Please write "PVDP help" in the subject. 

<a name="Citation"></a>
## Citation
If you use PVDP in your research, please include the following reference: Gutierrez et al. (2020) To be published.
