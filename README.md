## Table of contents

1. [Introduction](#Welcome)

   1.1. [Data types](#Prerequisites)__
   1.2. [Pipeline](#Pipeline)  
   1.3. [Performance](#Performance)
   
2. [Installation](#Installation)

   2.1. [Prerequisites](#Prerequisites)
   
   2.2. [Downloading project](#Downloading)
  
3. [Tutorial](#Tutorial)



### Welcome

>Although Colombia has a demanding virus certification program monitored by the ICA, it is estimated that only 3-5% of the planting material used is certified. This project aims to generate a virus diagnostic platform that supports integrated viral disease management programs in Antioquia, with a view to improving productivity and environmental sustainability.

The viral detection package was developed in Python and uses the BLAST tool for viral identification. A curated database and optimized parameters are used.

### Prerequisites

Please go to official [BLAST](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) page and install the correct version for you operative system. To verify that the tool works correctly, enter the command terminal and type: *blastn*

The installation was successful if you get the following message:

```markdown
BLAST query/options error: Either a BLAST database or subject sequence(s) must be specified
Please refer to the BLAST+ user manual.
```

### Dependencies

```markdown
[Python](https://www.python.org/downloads/) 3.7 or higher
```
```markdown
Other packages:
-Plotly
-etc
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

### Supported files

The tool was developed for the analysis of RNA-seq data. The files can be single or paired, they can also be in FASTQ, FASTQ.GZ or FASTA format.

### Running the script

First open the command terminal and go to the folder where the downloaded files are located. The main script is called ***VirusDetectionPlatform_v1.py***. Copy the following line of text into the terminal:
```markdown
python3 VirusDetectionPlatform_v1.py file1.fastq file2.fastq*
```
File1.fastq and file2.fastq correspond to the name of the files that will be analyzed. Then press enter and please be patient.

The average time for a paired file of four gigabytes (eight gigabytes in total) is two and a half hours.


### Support or Contact

Having troubles? Please contact us.
