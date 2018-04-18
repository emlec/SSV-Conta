# SSV-Conta

**Package containing all scripts needed to quantify and characterize DNA contaminants from gene therapy vector production after NGS sequencing.** 

## Principle

The five scripts used are : 

* **Quade** : Fastq files demultiplexer, handling double indexing, molecular indexing and filtering based on index quality (python 2.7)
* **Sekator** : Multithreaded quality and adapter trimmer for PAIRED fastq files (Python2.7/Cython/C)
* **fastq_control_sampler** : Generate control FASTQ files (C)
* **RefMasker** : Hard mask homologies between fasta reference sequences identified by Blastn (python 2.7)
* **ContaVect** : Quantify and characterize DNA contaminants (python 2.7)



## Get SSV-Conta

Clone the repository SSV-Conta
```bash
git clone --recurse-submodules URL
```
Detailed information concerning the installation of Quade, Sekator, RefMasker and ContaVect is available in each README.
For ContaVect, install a version of pysam < v0.13.0. 

Make a link to bin 

## Usage 

### Pre-processing of sequencing reads
Input : chunks of non demultiplexed raw fastq files 

* In the folder where fastq files will be created, create the template : ```Quade.py -i```
After filling, run Quade :  ```Quade.py -c Quade_conf_file.txt```

Be careful : All the chunks path should be separated by tab or space. 
The version of this report doesn't include the Undetermined in the count of the pair passed and failed quality.

It can run several hours.

Output : Fastq demultiplexed (filtering based on index quality) +  Quade_report 

* In the folder where fastq files will be created, create the template : ```Sekator.py -i```
After filling, run Sekator : ```Sekator.py -c Sekator_conf_file.txt```

Be careful : If necessary create the library AdapterTrimmer.so required for the adapter trimming step :
```python setup.py build_ext --inplace```and then ```make clean```

Output : Fastq trimmed

### Create the FASTQ files of the in silico control

* Run the program fastq_control_sampler

### Mapping reads to reference sequences

* In the folder analysis, copy and fill the template present directly in ContaVect.

Run ```ContaVect.py Conf.txt```


## Authors and Contact

    Adrien Leger aleg@ebi.ac.uk @a-slide
    Emilie Lecomte emilie.lecomte@univ-nantes.fr @emlec


