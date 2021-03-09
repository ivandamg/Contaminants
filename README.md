

# 1 . IDENTIFY BATERIA ENDOSYMBIONTS

 1. Identify contaminants of genome assemblies with MASH  https://mash.readthedocs.io/en/latest/



       /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/Soft/mash-Linux64-v2.2/mash sketch -o References_glomero6 *
       
       
2. Screen genomes against MASH refSeq db

The fields ouptut are [identity, shared-hashes, median-multiplicity, p-value, query-ID, query-comment]:

       /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/Soft/mash-Linux64-v2.2/mash screen -w -p 16 /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/10_Contaminants/00_GeneBank_Complete_Bacteria/Reference_GeneBank_2549_Bacteria_completeGenomes.msh 01_Genomes/Rclarus_HR1_GCA003203555.1.fna.gz > 03_BacteriaContaminants_Glomeromycetes/Screen_RefSeqk21S1000_Rclarus.tab
       
       
       IN loop
       
      for i in $(ls *.fna.gz); do echo $i; /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/Soft/mash-Linux64-v2.2/mash screen -w -p 16 /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/10_Contaminants/00_GeneBank_Complete_Bacteria/Reference_GeneBank_2549_Bacteria_completeGenomes.msh $i > ../03_BacteriaContaminants_Glomeromycetes/Screen_RefSeqk21S1000_$(echo $i | cut -d'_' -f1,2,3).tab ; done 
       
       
 2b. Screen Narnella on Bacterial genomes
 
   for i in $(ls *.fna.gz); do echo $i; /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/Soft/mash-Linux64-v2.2/mash screen -w -p 16 /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/10_Contaminants/00_GeneBank_Complete_Bacteria/Reference_GeneBank_2549_Bacteria_completeGenomes.msh $i > ../03_BacteriaContaminants_Glomeromycetes/Screen_RefSeqk21S1000_$(echo $i | cut -d'_' -f1,2,3).tab ; done 
 

3. Add file name to the end of string and concatenate all files

              for i in $(ls *.tab); do echo $i; sed "s/.*/&\\t$(echo $i |cut -d'.' -f1 | cut -d'_' -f3,4,5)/" $i > tmp ; mv tmp ScreenV2_$(echo $i |cut -d'.' -f1 | cut -d'_' -f3,4,5).tab; done
              
              cat ScreenV2_* > ALL_Glomeromycota_Screen_v1.out
              
4. move to local to vizalize with R
using script :Containment_detection_script_v1.R


# 2 Extract genome of endosymbiont from raw reads. denovo assembly with metaSPAdes 
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5411777/

    de novo assembly with SPADES http://cab.spbu.ru/files/release3.13.0/manual.html#sec3.5

     /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/Soft/SPAdes-3.15.1-Linux/bin/metaspades.py -1 GC067279_R1_fastq.gz_trimmed.fq.gz  -2 GC067279_R1_R2_fastq.gz_trimmed.fq.gz  -k 21,33,55,77 -o 01_A1_MetaSPAdes/

for all files

            for i in $(ls *_R1_val_1.fq.gz); do echo $i ; ~/Documents/software/SPAdes-3.13.0-Linux/bin/spades.py -1 $i  -2 $(echo $i | cut -d'_' -f1)_R2_val_2.fq.gz   -k 21,33,55,77,99,127 --careful --cov-cutoff auto -o 03_denovoAssembly/$(echo $i | cut -d'_' -f1)/ ; done

3b. denovo plasmid assembly



# 3. Identify if endosymbiont present in other fungi. identify in which clade is always present.

# 4 compare genome to the one of bettles and other organisms.


#5. Comparison of gene expression in different structures of AMF KAMEOKA.


