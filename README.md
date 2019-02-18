# AdvInformatics_Lab6
First lab with Tony

# EE283 Lab

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

End up with:

```
P004_R1.fq.gz  P015_R1.fq.gz  P029_R1.fq.gz  P043_R1.fq.gz  P051_R1.fq.gz
P004_R2.fq.gz  P015_R2.fq.gz  P029_R2.fq.gz  P043_R2.fq.gz  P051_R2.fq.gz
P005_R1.fq.gz  P019_R1.fq.gz  P030_R1.fq.gz  P044_R1.fq.gz  P058_R1.fq.gz
P005_R2.fq.gz  P019_R2.fq.gz  P030_R2.fq.gz  P044_R2.fq.gz  P058_R2.fq.gz
P006_R1.fq.gz  P020_R1.fq.gz  P034_R1.fq.gz  P045_R1.fq.gz  P059_R1.fq.gz
P006_R2.fq.gz  P020_R2.fq.gz  P034_R2.fq.gz  P045_R2.fq.gz  P059_R2.fq.gz
P013_R1.fq.gz  P021_R1.fq.gz  P035_R1.fq.gz  P049_R1.fq.gz  P060_R1.fq.gz
P013_R2.fq.gz  P021_R2.fq.gz  P035_R2.fq.gz  P049_R2.fq.gz  P060_R2.fq.gz
P014_R1.fq.gz  P028_R1.fq.gz  P036_R1.fq.gz  P050_R1.fq.gz  README.ATACseq.txt
P014_R2.fq.gz  P028_R2.fq.gz  P036_R2.fq.gz  P050_R2.fq.gz
```

Then I can pair the README with the file names using:

```
for file in  $(ls *.fq.gz)
do
  echo mv ${i} $(grep $(echo $i | cut -f1 -d"_") README.ATACseq.txt | awk '{print $2}')_$(echo $i | cut -f2 -d"_")
done
```

# RNAseq

I decided that it would be best to get the files out of the sub-directories they are in to simplify the paths.

```
find /pub/tbatarse/Bioinformatics_Course/RNAseq/RNAseq384plex_flowcell01/ -type f -print0 | xargs -0 mv -t /pub/tbatarse/Bioinformatics_Course/RNAseq/
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

End up with:

```
A4_1_1.fq.gz  A4_3_2.fq.gz  A5_3_1.fq.gz  A6_2_2.fq.gz  A7_2_1.fq.gz
A4_1_2.fq.gz  A5_1_1.fq.gz  A5_3_2.fq.gz  A6_3_1.fq.gz  A7_2_2.fq.gz
A4_2_1.fq.gz  A5_1_2.fq.gz  A6_1_1.fq.gz  A6_3_2.fq.gz  A7_3_1.fq.gz
A4_2_2.fq.gz  A5_2_1.fq.gz  A6_1_2.fq.gz  A7_1_1.fq.gz  A7_3_2.fq.gz
A4_3_1.fq.gz  A5_2_2.fq.gz  A6_2_1.fq.gz  A7_1_2.fq.gz  README.DNA_samples.txt
```
