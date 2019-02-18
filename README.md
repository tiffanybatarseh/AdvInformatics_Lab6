# AdvInformatics_Lab6
First lab with Tony

# EE283 Lab Notes

Determine how to organize the files.
Determine the best way to organize it and write a script to organize them in the way that you find best.

# ATACseq

I can remove the barcodes that aren't necessary to identify the file. The first field in the filename can be used to identify the file with the biological information found in the readme file.

```
for filename in *.fq.gz; do
    [ -f "$filename" ] || continue
    mv "$filename" "${filename//Sample*L1_/}"
done
```

Then I can pair the README with the file names using:

```
for i in  $(ls *.fq.gz)
do
  mv ${i} $(grep $($i | cut -f1 -d"_") README.ATACseq.txt | awk '{print $2"_"$3"_"$4}')_$($i | cut -f2 -d"_") 
done
```

# RNAseq

I decided that it would be best to get the files out of the sub-directories they are in to simplify the paths.

```
find /pub/tbatarse/Bioinformatics_Course/RNAseq/RNAseq384plex_flowcell01/ -type f -print0 | xargs -0 mv -t /pub/tbatarse/Bioinformatics_Course/RNAseq/
```

```
for i in  $(ls *.fastq.gz)
do
  echo mv ${i} $(grep $(echo $i | cut -f1 -d"_") RNAseq384_SampleCoding.txt | awk '{print $5"_"$8"_"$12}')_$(echo $i | cut -f4 -d"_") 
done
```

# DNAseq

Rename the sequencing center's arbitrary scheme to the biological sample's identifier.

```
for i in ADL06*
do
    mv "$i" "${i/ADL06/A4}"
done
```

```
for i in ADL09*
do
    mv "$i" "${i/ADL09/A5}"
done
```

```
for i in ADL10*
do
    mv "$i" "${i/ADL10/A6}"
done
```

```
for i in ADL14*
do
    mv "$i" "${i/ADL14/A7}"
done
```
