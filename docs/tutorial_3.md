## 1. What do genomic sequences look like on my computer?

A genomic sequence is any sequence that has been extracted from a genome. <br>
🐞 It could be a gene, a protein or a non-coding element (like a regulatory region).

These DNA sequences are often saved as a text file that can have multiple formats - the most common format for evolutionary analyses is **FASTA**.


> [!IMPORTANT]  
> A FASTA file is made up of two elements:
> * header: a line at the beginning of the sequence that tells you information about it. The header is formed by the symbol `>` followed by a line of text.
> * sequence: the actual sequence of nucleotides or amino acids that make up that gene, protein, or non-coding element. The sequence starts on the line immediately below, and usually there's a line break every 60-80 characters. 

> ```
> >XM_019925131.2:314-2584 PREDICTED: Tursiops truncatus forkhead box P2 (FOXP2), mRNA`
> ATGATGCAGGAATCTGCGACAGAGACAATAAGCAACAGTTCAATGAATCAAAATGGAATGAGCACTCTAA`
> GCAGCCAATTAGATGCTGGCAGCAGAGATGGAAGATCAAGTGGTGACACCAGCTCTGAAGTAAGCACAGT`
> ```
>

## 2. Downloading genomic sequences

In our tutorials, we will analyze the coding sequences of the **FOXP2 gene**. 
* Our goal is to investigate how FOXP2 evolved in mammals that are capable of vocal learning (like us!). 
* For that, first we need to obtain **our data set**: a collection of FOXP2 sequences for different mammal species. 
* We will download these sequences from **[NCBI](https://www.ncbi.nlm.nih.gov/)**, one of the most widely used genomic databases.

🐞 To download our FOXP2 sequences, we need to know the **names of the species** and the **accession numbers** of each sequence. Accession numbers are how NCBI keeps track of each sequence in their database, each individual sequence has one. \
Our data set will include the following 10 species:
* Human (_Homo sapiens_) | NM_014491.4
* Chimpanzee (_Pan troglodytes_) | XM_063813769.1
* Cow (_Bos taurus_) | NM_001205569.3
* Bottlenose dolphin (_Tursiops truncatus_) | XM_019925131.2
* Killer whale (_Orcinus orca_) | XM_049715204.1
* Harbor Seal (_Phoca vitulina_) | XM_032401732.1
* Dog (_Canis lupus familiaris_) | XM_038439870.1
* Little brown bat (_Myotis lucifugus_) | XM_023760067.1
* African elephant (_Loxodonta africana_) | XM_023544567.1
* Manatee (_Trichechus manatus latirostris_) | XM_004382567.2

> [!IMPORTANT] 
> Ok, so how do we download these sequences from NCBI into our computer, so we can work with them? <br> 
> There are two main ways: 
> * using a graphic interface on their website or 
> * the command-line prompt on your terminal. 

We will start nice and easy, with the graphic interface. <br>
Then, we will learn about the command-line version, which is **essential** if you are interested in working with coding sequences.

### 🍄 Downloading sequences from NCBI Nucleotide
1. Go to NCBI 
2. Search for the gene name, `FOXP2`
[**Orthologs**](https://www.ncbi.nlm.nih.gov/datasets/gene/3077/#orthologs) visualizing tool (it's way easier to search!)
<img src="https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/91b11fcc-f0e5-454f-961b-c78467fcb74b" width="800">
 
4. Use the option **Search the Taxonomy Tree** to filter for the group you are interested in (in this case, Placental mammals should work).
* select the species you want to download by clicking on the empty white box beside their names. <br>
* click on `Download > RefSeq Transcripts (FASTA) > One sequence per gene` to get a FASTA file containing all your sequences of interest.

<img src="https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/2e40e2e8-dc9f-487e-85fa-eeebedd158c6" width="800">

5. Your downloaded sequence file should have a name like: `FOXP2_refseq_transcript.fasta`. Save it in the `tutorial_3` folder on your computer. 

---
### 🍄 Pause for a deep breath

Brace yourself: take a deep breath, because things will get a little more complicated - but it's nothing you can't master with practice!

<img src="https://github.com/user-attachments/assets/7f2c1553-314d-478b-9b30-3ff36d9df453" width="300">

---

### 🍄 Downloading sequences using command-line

We will now learn how to download genomic sequences using command-line. <br>
This is currently the best way to download a set of **coding sequences**, which you can analyze in codon models such as **codeml**.

This part of the tutorial was adapted from NCBI's own tutorial: [Get one protein per gene from a set of orthologs](https://www.ncbi.nlm.nih.gov/datasets/docs/v2/tutorials/ortholog-get-one-isoform/). Feel free to check it out for more details!

⒈ Access our lab server, Awarnach (for a reminder, please check [Tutorial 2](https://github.com/Evolution-for-Everyone/bioinformatics-for-everyone/wiki/Tutorial-2:-Working-on-a-server))

⒉ Activate the environment where `ncbi_datasets` is installed by running:
```bash
source activate ncbi_datasets
```
⒊ Navigate to your `tutorial_3` folder using `cd` followed by the pathway to the folder:
```bash
cd tutorials_2025/tutorial_3/
```
> [!NOTE]
> **Pause to explain the next steps** <br>
> * Because many genes undergo alternative splicing, they have multiple transcript variants (mRNA isoforms). 
> * They all come from the same gene, but their coding sequences and sizes can be different.
> * In most comparative genomic studies, we only need one sequence per gene - so it's our job to "choose" the most representative transcript to include in our data set.
> * The overall convention is to select the longest transcript, which will most likely contain the entire coding sequence of that gene.

⒋ We will now **download only the longest transcript** of FOXP2 for each species! <br>
For each step below, just copy and paste the commands on your terminal, then hit Enter (_but make sure to read and understand what they are doing_).

🐛 This part can be challenging for beginners, so every step you complete you will unlock a celebratory cat GIF. \
**YOU GOT THIS!!**

<img src="https://github.com/user-attachments/assets/a5450877-37d5-4e5c-ace8-7ca774857788" width="300">

**🐞 Getting FOXP2 metadata** \
We will enter the `datasets summary` command to recover metadata about the FOXP2 sequences we are interested in. \
As input, will use the accession numbers of our 10 sequences (from the beginning of the tutorial). \
This command prints out a data report in the json-lines format: `foxp2_orthologs.jsonl`.

```bash
datasets summary gene accession \
NM_014491.4 XM_063813769.1 NM_001205569.3 XM_019925131.2 XM_049715204.1 XM_032401732.1 XM_038439870.1 XM_023760067.1 XM_023544567.1 XM_004382567.2 \
--report product --as-json-lines > foxp2_orthologs.jsonl
```

>[!NOTE]
> Metadata is anything that provides context or information about the data itself. In the case of NCBI sequences, the metadata includes:
> * common gene name 
> * gene ID (an identifier unique to each gene)
> * name of the species/taxon
> * sequence accession number
> * sequence length

<details>

<summary>WELL DONE! Click to unlock celebratory cat #1</summary>

<img src="https://i.pinimg.com/originals/61/79/3d/61793d8588130c2ea05abb955326c5d3.gif" width="200">

</details>

**🐞 Extracting information about sequence length** \
We will use the `dataformat` command to extract the [Gene Product Report](https://www.ncbi.nlm.nih.gov/datasets/docs/v2/reference-docs/data-reports/gene-product/) from our jsonl file, and convert it into a readable table in the `tsv` format. \
We want the Gene Product Report because it contains information about FOXP2's transcripts and proteins. \
Note that the `--fields` option is specifying the information we want to include in our table, such as gene id, symbol, transcript length etc.

```bash
dataformat tsv gene-product \
--inputfile foxp2_orthologs.jsonl \
--fields gene-id,tax-name,symbol,transcript-accession,transcript-length,transcript-protein-accession,transcript-protein-length > transcript_protein.tsv
```

Let's take a look at this table! For that, we will use the command `head`, which displays the first 10 lines of a file. It's very useful for taking a quick look at long files. 

```bash
head transcript_protein.tsv
```

The beginning of your table should look like this:
```bash
NCBI GeneID	Taxonomic Name	Symbol	Transcript Accession	Transcript Transcript Length	Transcript Protein Accession	Transcript Protein Length
93986	Homo sapiens	FOXP2	NR_033766.2	6355		
93986	Homo sapiens	FOXP2	NR_033767.2	6601		
93986	Homo sapiens	FOXP2	NM_148898.4	6618	NP_683696.2	740
93986	Homo sapiens	FOXP2	NM_148900.4	6594	NP_683698.2	732
93986	Homo sapiens	FOXP2	NM_014491.4	6543	NP_055306.1	715
93986	Homo sapiens	FOXP2	NM_001172766.3	6540	NP_001166237.1	714
93986	Homo sapiens	FOXP2	NM_001172767.2	1485	NP_001166238.1	457
93986	Homo sapiens	FOXP2	NM_148899.3	1410	NP_683697.2	432
449627	Pan troglodytes	FOXP2	XM_063813769.1	4716	XP_063669839.1	764
```
📍 Let's break down this table:
* The first line of contains the column headers: NCBI GeneID, Taxonomic Name, Symbol, Transcript Accession, Transcript Transcript Length, Transcript Protein Accession, Transcript Protein Length
* The columns are separated by a `tab`, so we have 7 columns
* The first column contains the GeneID, the second has the taxon name, the third has the gene name (referred to as "symbol"), and so on.
  * can you find which column has the accession numbers of the transcripts? What about protein length?

<details>

<summary>GREAT WORK! Click to unlock celebratory cat #2</summary>

<img src="https://i.pinimg.com/originals/e1/c6/82/e1c6829221cf788ca7384af54b9b94ee.gif" width="300">

</details>

**🐞 Making a list of the longest sequences** \
Now we will use a bash script to locate the longest FOXP2 transcripts and proteins of each species and save their accession numbers into a list. The accession numbers will allow us to identify these sequences and download them later. 

📍Since this is a large script, it's safer to save it as a file, then run it. Create a new file by entering:

```bash
nano list_longest.sh
```

Once your text editor is open, copy the script below and paste it on the terminal screen using `Ctrl+V`. \
PS: don't get scared! Above each line of the script, you will find a comment starting with `#` explaining what it does.

```bash
# Removes the first line (header) from the file and passes the rest to the next command
tail -n +2 transcript_protein.tsv | \
# Extracts the first column (gene IDs)
cut -f1 | \
# Sorts gene IDs alphabetically and removes duplicates
sort -u | \
# Reads each unique gene ID one by one
while read GENE_IDS; do

        # Searches for lines where the first column matches the gene ID
        LONGEST=$(grep -w "^$GENE_IDS" transcript_protein.tsv | \
        # Sorts the filtered lines numerically (-n), in descending order (-r), based on column 7 (protein length)
        sort -t$'\t' -nr -k7 | \
        # Selects the top row (the transcript with the longest protein sequence)
        head -n1 | \
        # Extracts column 4 (transcript ID) and column 6 (protein ID)
        cut -f4,6 | \
        # Converts the tab-separated values into newline-separated values
        tr '\t' '\n');

        # Appends the transcript ID and protein ID of the longest transcript to longest.list
        printf "$LONGEST\n" >> longest.list;

done
````

Now, we can run the script by entering `bash list_longest.sh`. This command tells the terminal to interpret our script file using the bash language.

📍 After running successfully, your script should have created a file named `longest.list`. Let's take a look at it!
```bash
cat longest.list
```

You should see on your screen the accession numbers of the longest transcripts and proteins, like this:

```bash
XM_023544567.1
XP_023400335.1
XM_049715208.1
XP_049571165.1
XM_019925131.2
XP_019780690.1
XM_004382567.2
XP_004382624.1
XM_023760067.1
XP_023615835.1
XM_032401732.1
XP_032257623.1
XM_063813769.1
XP_063669839.1
XM_038687039.1
XP_038542967.1
XM_015469121.3
XP_015324607.1
NM_148898.4
NP_683696.2
```

<details>

<summary>ALMOST THERE! Click to unlock celebratory cat #3</summary>

<img src="https://i.pinimg.com/originals/40/45/1e/40451ec95d906f7c739cf21038dca0b6.gif" width="300">

</details>

**🐞 Downloading the longest sequences**\
Finally, it's time to download the longest transcripts (AKA your data set)! <br>
We will use the `datasets download` command to download our list of longest transcripts from the NCBI database. <br>

```bash
datasets download gene accession \
--inputfile longest.list \
--fasta-filter-file longest.list \
--include rna,cds,protein \
--filename longest.zip
```

After running this command, you will see some updates on your screen:
```bash
Collecting 10 gene records [================================================] 100% 10/10
Downloading: longest.zip    33.5kB valid zip structure -- files not checked
Validating package [================================================] 100% 7/7
```
If you see the bar get to 100%, it means that the download was successful! The results will come out as a zip file called `longest.zip`. 

📍 Now it's time to look at our downloaded sequences! For that, let's unzip the `longest.zip file`:
```bash
unzip longest.zip
```
After entering the command, you will get this message:
```bash
Archive:  longest.zip
  inflating: README.md               
  inflating: ncbi_dataset/data/rna.fna  
  inflating: ncbi_dataset/data/cds.fna  
  inflating: ncbi_dataset/data/protein.faa  
  inflating: ncbi_dataset/data/data_report.jsonl  
  inflating: ncbi_dataset/data/dataset_catalog.json  
  inflating: md5sum.txt 
```
Now, if you list (`ls`) what's inside your current folder, you will notice a new folder called `ncbi_dataset`. Let's see what's inside it:
```bash
ls ncbi_dataset
```
Inside `ncbi_dataset` there's a folder called `data`. To find out what's inside `data`, we can use the same `ls` command, followed by the pathway to `data`:
```bash
ls ncbi_dataset/data
```
You should see the following files: `cds.fna  data_report.jsonl  dataset_catalog.json  protein.faa  rna.fna`

<img src="https://i.pinimg.com/originals/20/ee/a8/20eea82d92e4b972c25d8b55455aa921.gif" width="400"> 

**🌺 And there's our data!!** \
The sequence data of the FOXP2 gene is contained in 3 files:
* `rna.fna` contains all the longest transcripts
* `protein.faa` file contains the longest corresponding proteins
* `cds.fna` (which will be super important in the next tutorials) contains the same sequences, but only the coding portion (so no regulatory/flanking sequences)! 

Using `head`, take a look at the first lines of these 3 files. \
**But watch out!** Right now, you re inside `tutorial_3`, and your files are in `ncbi_dataset/data`. Now there's two ways you can do the command correctly:
* Navigate to `data`, and then use `head`:
```bash
cd ncbi_dataset/data
head rna.fna
```
* Use the `head` command from your current folder, passing the pathway to the input files:
```bash
head ncbi_dataset/data/rna.fna
```
You can choose what way you prefer! Do this for all 3 files. \
After entering the command, the first lines of your `rna.fna` file should be:
```bash
>XM_015469121.3 FOXP2 [organism=Bos taurus] [GeneID=505502] [transcript=X1]
GGACCTGGCAGAGTCCCCACGGACGAGAGCGGGACTCGGGCGCTGGAGGCTGGGCCCGCGCACTCCCCAC
GCCGGCGTCTCGGCTTTGAAGTGCGAGCGGCAGTTCTGGCAGTTTCTTCTTTCCTTTCATTCCGGTTACT
TTGCTCCCCTCAGTCACTGACAGGCCCGTCTCGAGAGCCTCAGACCCCCAAAGTCTCAGCTCGGCAACCC
CTTCCTTCTAAGCTCCGCCCCGGCCGAACCGCAGCCCGGCGCCGAGCCGGTGACCAGGGCTGGGGGATCA
CGAGGAAGCCCGAGAACTCCCGGGTCCAAGTGAGACAGGAGCCCGACAACAATGAAGAGTGAGAAAGACA
CTCGGCCTCTCCACCCCAGGCCGCAGAGGCGCACACCGCGAAAAGAAAGGCCAGTCAGCGTTTTAACGCA
CGCTTGGGTCTCCCTTTCTGACTCTCGAGTACTTTAACTCCTTGCCACCGAGGGCTTTGGATCCCTTCGA
GGCTTCCTGCACTTCACTTGGAATTCCCTGTTTCATTTGCCAGCAGCTCCGTCTGCTGAGAGGACGTACT
TTAGGGACTGCCAAGAAGCAGCAGACACAACTCAGCTTTGCCAATACAGCATAAGGTTTTGTTCTCTCCT
```
and the first lines of your `protein.fna` file:
```bash
>XP_015324607.1 FOXP2 [organism=Bos taurus] [GeneID=505502] [isoform=X1]
MMQESATETISNSSMNQNGMSTLSSQLDAGSRDGRSSGDTSSEVSTVELLHLQQQQALQAARQLLLQQQT
SGLKSPKSSDKQRPLQELLPETKLCVCGHSSGDGHPHNTFAVPVSVAMMTPQVITPQQMQQILQQQVLSP
QQLQALLQQQQAVMLQQQQLQEFYKKQQEQLHLQLLQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQQP
QQQHPGKQAKEVGSGQLIHAEEREQQQQQLAAQQLVFQQQLLQMQQLQQQQHLLSLQRQGLISIPPGQAA
LPVQSLPQAGLSPAEIQQLWKEVTGVHSMEDNGIKHGGLDLTTNNSSSTTSSTTSKASPPITHHTIVNGQ
SSVLNARRDSSSHEETGASHTLYGHGVCKWPGCESICEDFGQFLKHLNNEHALDDRSTAQCRVQMQVVQQ
LEIQLSKERERLQAMMTHLHMRPSEPKPSPKPLNLVSSVTMSKNMLETSPQSLPQTPTTPTAPVTPITQG
PSVITPASVPNVGAIRRRHSDKYNIPMSSEIAPNYEFYKNADVRPPFTYATLIRQAIMESSDRQLTLNEI
YSWFTRTFAYFRRNAATWKNAVRHNLSLHKCFVRVENVKGAVWTVDEVEYQKRRSQKITGSPTLVKNIPT
```
and here are the first lines of the `cds.fna` file:
```bash
ATGATGCAGGAATCTGCGACAGAGACAATAAGCAACAGTTCAATGAATCAAAATGGAATGAGCACTCTAA
GCAGCCAATTAGATGCTGGCAGCAGAGATGGAAGATCAAGTGGTGACACCAGCTCGGAAGTAAGCACAGT
AGAACTGCTGCATCTGCAACAACAGCAGGCTCTCCAAGCAGCGAGACAACTTCTCTTACAGCAGCAAACA
AGTGGATTGAAATCTCCTAAGAGCAGTGATAAACAGAGACCACTGCAGGAATTGCTTCCAGAAACAAAAT
TATGTGTCTGTGGCCACTCTTCTGGTGATGGGCATCCTCACAACACATTTGCAGTGCCCGTGTCAGTGGC
CATGATGACTCCCCAGGTGATCACCCCTCAGCAAATGCAGCAGATCCTTCAGCAGCAAGTCCTGTCTCCT
CAGCAGCTCCAAGCCCTCCTTCAGCAGCAGCAGGCAGTCATGCTGCAGCAGTCAAAATGGTTTATTCAGC
AACAACTACAAGAGTTTTACAAGAAACAGCAAGAGCAGTTACATCTTCAGCTTTTGCAGCAGCAGCAACA
GCAGCAGCAGCAGCAGCAGCAGCAGCAACAGCAGCAGCAGCAGCAGCAGCAGCAACAGCAGCAGCAGCCC
```

**Do these sequences remind you of the `fasta` format we talked about in the beginning?** \
Well, there you go! You have just downloaded your first genomic sequences in `fasta` format 🌺

**Do you notice any differences between these 3 sequences?How are they different?**

## 3. Preparing sequences for analysis

### 🍄 Editing the headers of a fasta file

```bash

awk -F' ' '
/^>/ {
    gene = $2                          # Extract second field (FOXP2)
    sub(/\[organism=/, "", $3)         # Remove "[organism=" from third field
    org = substr($3, 1, 1)             # Take the first letter (C)
    sub(/\]/, "", $4)                  # Remove closing bracket if present
    ending = substr($4, 1, 3)          # Take first three letters (lup)
    print ">" gene "_" org ending      # Output formatted header
    next                               # Skip further processing for header lines
}
{print}  # Print sequence lines unchanged
' cds.fna > cds_headers.fna
```