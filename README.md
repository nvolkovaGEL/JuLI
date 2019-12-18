<p align="center">
  <a href="">
    <img height="150" src="https://github.com/sgilab/JuLI/blob/master/JuLI_logo.png">
  </a>
  <h1 align="center">Junction Location Identifier (JuLI)</h1>
</p>


Installing JuLI
----------------
Download https://github.com/sgilab/JuLI/raw/master/JuLI-0.1.3.zip

Unzip JuLI-X.X.X.zip (type the downloaded version)

Open R (>= 3.3.1)

    install.packages('devtools') # install library for installation
    
    library(devtools) # load library
    
    setwd('/path/JuLI-vX.X.X') # set download path
    
    install('julivX.X.X') # install JuLI
  
  
Input of JuLI
----------------
Sorted BAM


Running JuLI
----------------
Open R (>= 3.3.1)

    library(julivX.X.X)

 *Function for call fusions
    
    callfusion(CaseBam='/InputPath/Input.bam',             
               TestID='TestID',           
               OutputPath='/OutputPath',     
               Thread=integer,         
               Refgene='/path/JuLI-vX.X.X/references/refGene_hg19.txt',          
               Gap='/path/JuLI-vX.X.X/references/gap_hg19.txt',
               Reference='/path/hg19.fa')

[Options]  
CaseBam: Path of case bam. If you want joint call from multiple bams, insert path of bams separated by comma (ex:CaseBam='/path/input1.bam,/path/input2.bam ...').  
ControlBam: Path of control bam.    
TestID: Name of sample. Default is a CaseBam name. If you want joint call, insert names separated by comma (ex:TestID='name1,name2 ...').  
OutputPath: Path of output. Default is a path of case bam.  
Thread: Thread number for parallel processing. Default is one thread.  
ControlPanel: Path of control panel. The panel is generated by JuLI's 'controlpanel' function.  
TargetBed: Path of target region file with BED format.  
Refgene: Path of gene information file from UCSC database. It is uploaded to JuLI's github.  
Gap: Path of gap information file from UCSC database. It is uploaded to JuLI's github.  
Reference: Path of reference fasta file.  
AnalysisType: Alignment type for analysis. Default is 'DP'. DP; discordant and proper pair, D; discordant pair only, P; proper pair only.  
AnalysisUnit: Analysis unit of each processing. Default is 1000.  
MinMappingQuality: Minimum mapping quality of analysis. Default is 0.  
SplitCutoff: Cutoff of split reads. Default is two.  
DiscordantCutoff: Cutoff of discordant reads. Default is three.  
NucDiv: Use of nucleotide diversity filter. Default is TRUE.  
SplitRatio: Split ratio cutoff of pairwise alignment. Default is 0.7.  
MatchBase: Sequence length cutoff of pairwise alignment. Default is 10bp.  
Log: Log file genereation. Default is FALSE.  


*Function for annotation fusions

    annofusion(Output='/OutputPath/TestID.txt',         
               Refgene='/path/JuLI-vX.X.X/references/Refgene_hg19.txt',            
               Cosmic='/path/JuLI-vX.X.X/references/CosmicFusionExport_V76.tsv',             
               Pfam='/path/JuLI-vX.X.X/references/Pfam-A.full.human',             
               Uniprot='/path/JuLI-vX.X.X/references/HGNC_GeneName_UniProtID_160524.txt')

[Options]  
Output: Path of callfusion output.  
Refgene: Path of gene information file from UCSC database. It is uploaded to JuLI's github.  
Cosmic: Path of cosmic data file. It is uploaded to JuLI's github.  
Pfam: Path of Pfam data file. It is uploaded to JuLI's github.  
Uniprot: Path of Uniprot data file. It is uploaded to JuLI's github.  


*Function for generation of control panel

    controlpanel(ControlBams=c('/path/control1.bam,/path/control2.bam ...'),
                 ID='ID',
                 OutputPath='/OutputPath',
                 Thread=integer)

[Options]  
ControlBams: Path of control bams separated by comma.  
ID: Name of control panel.  
OutputPath: Path of output.  
Thread: Thread number for parallel processing. Default is one thread.  



Output of JuLI
----------------
-	TestID.txt: raw output

-	TestID.annotated.txt: annotated output (strand specific event, flanking gene, frame, and cosmic)

-	TestID.annotated.gene.pdf: visualized gene-gene events with domain information

-	TestID.BamStat.txt: statistics of case bam

-	TestID.log: calling log (option)


Interpretation of JuLI
----------------
-	chrA,B: reference sequence names of each breaks

-	OriA,B: fusion orientation of breaks of each breaks

    0: 5 prime end of positive reference strand

    1: 3 prime end of positive reference strand

-	DisA,B: discordant reads count supporting each breaks

-	SplitA,B: split reads count supporting each breaks

-	Event: rearrangement type (e.g. deletion, inversion, tandem, interchromosomal_translocation)

-	GeneA,B: gene names of each breaks

-	StrGeneA,B: strand of each genes

-	Direction: fusion direction

-	Frame: prediction of reading frame status of chimeric transcripts

    Inframe: no frame change

    Outframe: frame chage

    Possible Outframe/inframe: frame prediction when breaks in exonic region

-	Cosmic: frequency of fusion events according cancer types


Test JuLI
----------------
Open R (>= 3.3.1)

    library(julivX.X.X)

    callfusion(CaseBam='/path/JuLI-master/test/JuLI_test.bam',         
               TestID='JuLI_test',           
               OutputPath='/path/JuLI-master/test',           
               Thread=1,         
               Refgene='/path/JuLI-master/references/refGene_hg19.txt',          
               Gap='/path/JuLI-master/references/gap_hg19.txt',
               Reference='/path/hg19.fa')

    annofusion(Output='/path/JuLI-master/test/JuLI_test.txt',        
               Refgene='/path/JuLI-master/references/refGene_hg19.txt',            
               Cosmic='/path/JuLI-master/references/CosmicFusionExport_V76.tsv',           
               Pfam='/path/JuLI-master/references/Pfam-A.full.human',          
               Uniprot='/path/JuLI-master/references/HGNC_GeneName_UniProtID_160524.txt')

