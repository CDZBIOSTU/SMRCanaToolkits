# function 1: calculate the proportion of each alternative splicing event in different samples and create graphs.
# function 2: calculate score_D of each gene.
# function 3: select top 500 genes and make GO enrichment analysis
----------------------------
## get_AS.py: calculate the proportion of each alternative splicing event in different samples and create graphs.
----------------------------

### Input files

An annotation file in GTF format is required (see e.g. http://mblab.wustl.edu/GTF22.html):

```
chr14 Ensembl exon  73741918  73744001  0.0 - . gene_id "ENSG00000000001"; transcript_id "ENST00000000001.1"; 
chr14 Ensembl exon  73749067  73749213  0.0 - . gene_id "ENSG00000000001"; transcript_id "ENST00000000001.1";  
chr14 Ensembl exon  73750789  73751082  0.0 - . gene_id "ENSG00000000001"; transcript_id "ENST00000000001.1"; 
chr14 Ensembl exon  73753818  73754022  0.0 - . gene_id "ENSG00000000001"; transcript_id "ENST00000000001.1"; 
```

### Usage
```
python3 get_AS.py options
```
List of options available:

- **-n**  | **--names**: names of GTF format file/files containing at least "exon" lines

- **-p**  | **--prefix**: prefix of output files

The command line to generate local AS events will be of the form:

```
python3 get_AS.py -n <names> -p <prefix>
```

### Output files

AS.txt
```
	A3	A5	AF	AL	MX	RI	SE
sample1	2131	2224	4850	1050	330	2652	4608
sample2	2638	2737	5562	1170	462	3130	5397
sample3	1689	1628	2911	431	261	2104	3267
sample4	2849	2666	6876	954	389	3851	4870
```

<img src="https://github.com/BioinformaticsSTU/SMRCanaToolkits/blob/master/CDZ/bar.png" width = "500" height = "400"  />
bar.png

<img src="https://github.com/BioinformaticsSTU/SMRCanaToolkits/blob/master/CDZ/barh_align.png" width = "400" height = "400"  />
barh_align.png

----------------------------
## get_score_D.py: calculate score_D of each gene.
----------------------------

### Input files

ioi file contains the transcript "events" in each gene.

### Usage
```
python3 get_score_D.py options
```
List of options available:

- **-c**  | **--control**: name of control sample

- **-t**  | **--treated**: name of treated sample

The command line to generate local AS events will be of the form:

```
python3 get_score_D.py -c <control> -t <treated>
```

### Output files

score_D.txt
```
	control_transcripts	treated1_transcripts	treated1_score	treated2_transcripts	treated2_score	
ENSG00000151466	ENST00000281142,ENST00000506368	ENST00000281142,ENST00000511426	0.667	ENST00000506368,ENST00000511426	0.667	1.334
ENSG00000128059	ENST00000264220	ENST00000264220	0	ENST00000264220	0	0
ENSG00000033178	ENST00000322244,ENST00000429659	ENST00000322244,ENST00000429659	0	ENST00000322244,ENST00000429659	0	0
ENSG00000145414	ENST00000274054	ENST00000274054	0	ENST00000274054	0	0
ENSG00000138767	ENST00000504123,ENST00000512485	ENST00000504123,ENST00000512485	0	ENST00000504804	1	1
```

To quantify the differential isoform usage between cells, we defined the score D of each gene as follows:

<img src="https://github.com/BioinformaticsSTU/SMRCanaToolkits/blob/master/CDZ/formula.png"  />



where gene j has isoform set a , and set b respectively in cell line X and Y ; c is the number of isoform intersection for set a and set b; d is the number of isoform union for set a and set b. Thus D sums up scores when comparing the control sample and treated samples.

----------------------------
## get_GO.py: select top 500 genes and make GO enrichment analysis
----------------------------

### Input files


### Usage
```
python3 get_GO.py options
```
List of options available:

- **-i**  | **--input**: score D result

- **-t**  | **--threshold**: threshold for adjusted p-value

- **-n**  | **--number**: number of top genes for analysis

- **-f**  | **--type**: type of image, 'bar' and 'scatter' can be chosen

The command line to generate local AS events will be of the form:

```
python3 get_GO.py -i <input> -t <threshold> -n <number> -f <type>
```




### Output files

GO_reports.txt
```
Gene_set	Term	Overlap	P-value	Adjusted P-value	Old P-value	Old Adjusted P-value	Z-score	Combined Score	Genes
GO_Biological_Process_2018	cellular response to DNA damage stimulus (GO:0006974)	26/330	9.13787228190808e-09	1.6576100319381273e-05	1.6286367911914452e-08	2.9543471392212826e-05	-1.3493239020889152	24.977116526080287	RPAIN;MUS81;BOD1L1;NUDT1;RECQL4;HERC2;RECQL5;CHEK2;MACROD1;NEK1;POLK;FNIP2;ZNF385A;VAV3;SHPRH;SLF1;DDX11;FANCA;RAD52;RNF168;RAD51B;PSME4;ATM;MMS19;CEP63;TP73
GO_Biological_Process_2018	regulation of striated muscle cell differentiation (GO:0051153)	3/9	0.0007078338095233947	0.18343007578220555	0.0015745180149574901	0.3173528532369876	-2.903223500208859	21.057954568005567	HDAC5;NRG1;HDAC9
GO_Biological_Process_2018	intraciliary retrograde transport (GO:0035721)	3/11	0.0013474224910073086	0.22220221806247806	0.0025281461092817154	0.36497538704896487	-2.67387109608216	17.67311619442282	DYNC2H1;ICK;DYNC2LI1
GO_Biological_Process_2018	double-strand break repair (GO:0006302)	11/142	0.00021322248264889278	0.09669639588127289	0.00028269216039523195	0.12820089473923768	-1.9459585449063224	16.4495269901104	RAD52;RECQL4;RNF168;RAD51B;HERC2;RECQL5;KDM4D;EME2;CHEK2;ATM;POLK
```

<img src="https://github.com/BioinformaticsSTU/SMRCanaToolkits/blob/master/CDZ/GO enrichment barh.png"  width="550" height="450" />
GO enrichment barh.png

<img src="https://github.com/BioinformaticsSTU/SMRCanaToolkits/blob/master/CDZ/GO enrichment scatter.png" width="550" height="400" />
GO enrichment scatter.png
