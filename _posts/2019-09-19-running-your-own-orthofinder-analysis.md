---
layout: post
title: "2. Running your own OrthoFinder analysis"
author: "David Emms"
categories: orthofinder_tutorials
tags: [documentation]
#fig_image: Figure3_ResultsData.png
#fig_caption: "Example figure to show the data generated by an OrthoFinder run"
---

Once you've downloaded OrthoFinder and checked you can run it on the Example Dataset then you're ready to run your own analysis!

## Plan for this tutorial
In this tutorial we're going to download the proteomes for the species we want to analyse and run OrthoFinder on those species. In the next tutorial we'll dive into the results. I downloaded OrthoFinder to a directory called '/home/david/orthofinder-tutorial/', if you downloaded it to somewhere else then change the paths in the commands as appropriate.

## Downloading proteomes for our species. 
In this tutorial we're going to perform a phylogenomic analysis across a set of model species: mouse, human, frog, zebrafish, fruit fly and *Caenorhabditis elegans*. For choosing the species to include in your own analysis see the post [Getting the most from your OrthoFinder analysis](/orthofinder_tutorials/getting-the-most-from-your-orthofinder-analysis.html).

1. Create a folder called "proteomes". It's best if there aren't any spaces in the path for this folder (e.g. "/home/david/orthofinder-tutorial/proteomes/" and not "/home/david/orthofinder tutorial/proteomes/").

2. Go to <https://www.ensembl.org/>. Click on "Human" under "Favourite genomes".

3. On the right hand side, under "Gene annotation" click "Download FASTA".
 <img src="{{ site.github.url }}/assets/img/ensembl_human_genome.png">
  Click on the "pep" folder and then download the file "Homo_sapiens.GRCh38.pep.all.fa.gz" to the folder you created.

4. Go back to the Ensembl main page and repeat for Mouse, Zebrafish, Tropical clawed frog (*Xenopus tropicalis*, under 'Amphibians'), *Drosophila melanogaster" and *C. elegans*. If the is a choice of files, chose the '.pep.all.fa.gz' file. 

5. Open a terminal and navigate to the directory that you downloaded the files to. The files are all compressed (they end in '.gz'), decompress them all using the command `gunzip *.gz`. 

6. The files from Ensembl will contain many transcript per gene. If we ran OrthoFinder on these raw files it would take 10x longer than necessary. We'll use a script provided with OrthoFinder to extract just the longest transcript variant per gene and run OrthoFinder on these files.
```
for f in *fa ; do python ~/orthofinder-tutorial/OrthoFinder/tools/primary_transcript.py $f ; done
```

7. Run OrthoFinder (if you haven't download and prepared the files yourself you can get them from here: [primary_transcripts.tar.gz]({{ site.github.url }}/assets/data/primary_transcripts.tar.gz).):
```
orthofinder -f primary_transcripts/
```

8. That's it! It will take from around 20 mins to a few hours to run, depending on how many cores you have and the speed of your machine. Assuming everything worked fine then the last few lines of OrthoFinder's output will look something like this:

```
Species-by-species orthologues directory:
   /home/emms/orthofinder-tutorial/proteomes/primary_transcripts/OrthoFinder/Results_Oct11/Orthologues/

Orthogroup statistics:
   Statistics_PerSpecies.tsv   Statistics_Overall.tsv   Orthogroups_SpeciesOverlaps.tsv

OrthoFinder assigned 116961 genes (89.4% of total) to 18098 orthogroups. Fifty percent of all genes were in orthogroups with 7 or more genes (G50 was 7) and were contained in the largest 5006 orthogroups (O50 was 5006). There were 4189 orthogroups with all species present and 1270 of these consisted entirely of single-copy genes.

CITATION:
 When publishing work that uses OrthoFinder please cite:
 Emms D.M. & Kelly S. (2015), Genome Biology 16:157

 If you use the species tree in your work then please also cite:
 Emms D.M. & Kelly S. (2017), MBE 34(12): 3267-3278
 Emms D.M. & Kelly S. (2018), bioRxiv https://doi.org/10.1101/267914

```

That's it! The next tutorial is: [Diving into the results](/orthofinder_tutorials/diving-into-the-results.html). If you haven't finished running OrthoFinder then you can download an archive of the results files from that tutorial.