# Contaminants


1. Identify contaminants of genome assemblies with MASH

       /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/Soft/mash-Linux64-v2.2/mash sketch -o References_glomero6 *
       
       
2. Screen genomes against MASH refSeq db


        /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/Soft/mash-Linux64-v2.2/mash screen -w -p 16 /scratch/wally/FAC/FBM/DEE/isanders/popgen_to_var/IM/Soft/mash-Linux64-v2.2/refseq.genomes.k21s1000.msh GCA_003203555.1_RclarusHR1_1.0_genomic.fna.gz > Screen_RefSeqk21S1000_Rclarus.tab
