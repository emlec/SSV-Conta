# SSV-Seq

**Package containing all scripts needed to quantify and characterize DNA contaminants from gene therapy vector production after NGS sequencing.** 

## Principle

The four scripts used are : 

* **Quade** : Fastq files demultiplexer, handling double indexing, molecular indexing and filtering based on index quality (python 2.7)
* **Sekator** : Multithreaded quality and adapter trimmer for PAIRED fastq files (Python2.7/Cython/C)
* **RefMasker** : Hard mask homologies between fasta reference sequences identified by Blastn (python 2.7)
* **ContaVect** : Quantify and characterize DNA contaminants


## Get SSV-Seq 

Clone each repository (Quade, Sekator, RefMasker, ContaVect) with --recursive option
```bash
git submodule add <Repository_name> 
git submodule update --init --recursive 
```
Make each script executable 
```bash
sudo chmod u+x <name.py>
```
Make a link to bin 

## Usage 

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

* In the folder references, create the template : ```RefMasker.py -i```.
After filling, run RefMasker : ```RefMasker.py -c RefMasker_conf_file.txt```

Be careful : If necessary install pyfasta package using ```sudo pip install pyfasta [--proxy name:port]

* In the folder analysis, copy and fill the template present directly in ContaVect.
There are no filtering, no trimming, and only one references indexing (for the first sample)

Run ```ContaVect.py Conf.txt```

In this version, the order of the "reference" sequences is not important. 



