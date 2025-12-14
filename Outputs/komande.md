# komande.md

*Ve�ba 6*

## >>> README.md

### 1.5 - 1.9 - uneti komande

```bash
tar -xzf za_vezbe_Klebsiella_sekvence.tar.gz
cd za_vezbe_Klebsiella_sekvence/
mkdir -p ../data/{genomes,annotations}
mv *.fna ../data/genomes
mv *.tff ../data/annotations
cd ..; mkdir results
```

---

## >>> klebsiella_demonstracija_prosirena.md

### 4.1 - uneti *output* komandi, a ne komande

```bash
# Upi�ite brojeve kolona koje izdvajate:
1    strain
71    virulence_score
52    iucA
60    iroB
67    rmpA
73    rmpA2

# Prika�ite izdvojene kolone za Strain, Virulence score, iucA, iroB, rmpA i rmpA2:
strain         iucA  iroB  rmpA     virulence_score  rmpA2
GCF_017743115  1     1     2        4                rmpA2_5-54%
GCF_017743135  9     6     11       4                -
GCF_017815715  1     1     2        3                rmpA2_5-54%
GCF_021057265  1     -     27       4                rmpA2_6*-47%
GCF_021442005  1     -     40*-47%  4                rmpA2_3-47%
GCF_902723695  1     1     2        4                rmpA2_2*-54%
GCF_902723705  1     1     2        4                rmpA2_4*-34%
GCF_902827215  2     4     82-19%   5                -
```

### 4.4 - uneti *output* komandi, a ne komande

```bash
# Upi�ite brojeve kolona koje izdvajate:
1    strain
71    virulence_score
98    resistance_score

# Prika�ite izdvojene kolone za Strain, Virulence score i Resistance score
strain         virulence_score  resistance_score
GCF_017743115  4                0
GCF_017743135  4                0
GCF_017815715  3                0
GCF_021057265  4                1
GCF_021442005  4                2
GCF_902723695  4                2
GCF_902723705  4                1
GCF_902827215  5                0

# Odaberite 1 soj koji je samo hipervirulentan (+ ima rmpA2):
GCF_017743115

# Upi�ite informaciju o njegovoj virulentnosti/rezistentnosti sa NCBI/Genome:
Sample details > Description: hypervirulent Klebsiella pneumoniae

# Odaberite 1 soj koji je hipervirulentan i multirezistentan (+ ima iroB):
GCF_902723695

# Upi�ite informaciju o njegovoj virulentnosti/rezistentnosti sa NCBI/Genome:
Sample details > Comment: Carbapenem resistant and hypervirulent Klebsiella pneumoniae kpn154
```

### 5.3 - uneti komande

```bash
cd ../data/annotations/
for file in *.gff; do
> echo "===$file==="
> grep -Ei "peg-344|iroB|iucA|rmpA|rmpA2" "$file" || echo "nijedan marker nije pronadjen"
> echo
> done
#svi fajlovi sadrze bar neki od markera
```

### 2 - uneti komande

```bash
cd ../..
mkdir klebsiella_genome
cd klebsiella_genome
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/GCF_021057265.1_ASM2105726v1_genomic.fna.gz
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/GCF_021057265.1_ASM2105726v1_genomic.gff.gz
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/md5checksums.txt
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/uncompressed_checksums.txt
gunzip -k GCF_021057265.1_ASM2105726v1_genomic.fna.gz
gunzip -k GCF_021057265.1_ASM2105726v1_genomic.gff.gz
grep "GCF_021057265.1_ASM2105726v1_genomic.fna.gz" md5checksums.txt > genome_compressed.txt
md5sum -c genome_compressed.txt #OK
```

### 3 - uneti komande

```bash
mkdir genomes; mkdir annotations
mv GCF_021057265.1_ASM2105726v1_genomic.fna genomes
mv GCF_021057265.1_ASM2105726v1_genomic.gff annotations
cd ..
tar -czf klebsiella_archive.tar.gz klebsiella_genome
tar -tzf klebsiella_archive.tar.gz 
```

### 4 - uneti komande i sadrzaj klebsiella_download_archive.sh fajla

```bash
mkdir scripts
touch scripts/klebsiella_download_archive.sh
cd scripts
nano klebsiella_download_archive.sh
#zatim se nalepe sve odgovarajuce komande u fajl:
#!/usr/bin/env bash
mkdir klebsiella_genome
cd klebsiella_genome
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/GCF_>
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/GCF_>
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/md5c>
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/021/057/265/GCF_021057265.1_ASM2105726v1/unco>
gunzip -k  GCF_021057265.1_ASM2105726v1_genomic.fna.gz
gunzip -k GCF_021057265.1_ASM2105726v1_genomic.gff.gz

mkdir genomes; mkdir annotations
mv GCF_021057265.1_ASM2105726v1_genomic.fna genomes
mv GCF_021057265.1_ASM2105726v1_genomic.gff annotations
cd ..
tar -czf klebsiella_archive.tar.gz klebsiella_genome
tar -tzf klebsiella_archive.tar.gz
#nastavak u terminalu
chmod +x klebsiella_download_archive.sh
#output prilikom pokretanja ./klebsiella_download_archive.sh unutar /scripts/:
klebsiella_genome/
klebsiella_genome/GCF_021057265.1_ASM2105726v1_genomic.gff.gz
klebsiella_genome/annotations/
klebsiella_genome/annotations/GCF_021057265.1_ASM2105726v1_genomic.gff
klebsiella_genome/md5checksums.txt
klebsiella_genome/uncompressed_checksums.txt
klebsiella_genome/GCF_021057265.1_ASM2105726v1_genomic.fna.gz
klebsiella_genome/genomes/
klebsiella_genome/genomes/GCF_021057265.1_ASM2105726v1_genomic.fna
```
