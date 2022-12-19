
```toc
```


### parsing paths

Use **ls** to retrieve folder names only, and then remove the trailing / character with **tr**

```sh
ls -d */ | tr -d / > file.txt
```

### csv to fasta

assuming you have a csv named sequences.csv with the first column as header and second column with sequence: 

```sh
awk -F , '{print ">"$1"\n"$2}' sequences.csv > sequences.fa
```

