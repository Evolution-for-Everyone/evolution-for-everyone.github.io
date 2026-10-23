## 1. Why align sequences?

Once we have extracted the gene sequences from NCBI, we need to align them.

!!! important "What does aligning mean?"
    Alignment arranges similar parts of sequences from different species so that we can compare them. In an alignment, each position is treated as descended from a common ancestral sequence.

🍄 There are many software programs for building multi-species alignments. Here we are going to learn about two popular ones: [MAFFT](https://mafft.cbrc.jp/alignment/server/) and [PRANK](http://wasabiapp.org/software/prank/#Translated_alignment_and_codon_alignment).

MAFFT is available online and from the command line, and we will learn how to use both. Then, we will also learn how to use PRANK from the command line.

## 2. Aligning with MAFFT

### 🍄 Using MAFFT online

1. Open the [MAFFT online server](https://mafft.cbrc.jp/alignment/server/).
2. Paste your entire sequence file into the text box, or upload it from your computer using **Choose file**.
3. Select your output formatting options.

   ![MAFFT output formatting options](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/52a2f08b-faf7-437c-886a-34fb99d7f541){ width="800" }

4. Select an alignment strategy and any other advanced options.

   * For relatively small data sets (fewer than 200 sequences), E-INS-i, L-INS-i, or G-INS-i may be suitable.
   * If you are unsure which options to use, the defaults are a reasonable starting point.

   ![MAFFT alignment strategy options](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/99adeb94-3f56-4975-a46f-2df638b31f02){ width="1000" }

5. Select **Submit**.
6. When the alignment is complete, the results page should have a **FASTA** button near the top. Select it to download the alignment in FASTA format, then save it in your `tutorial_4` folder with a meaningful name, such as `FOXP2_nuc_aligned_mafft.fasta`.

### 🍄 Using MAFFT on command line

1. Open a terminal and log in to your server account (Awarnach, Alliance, or another server).
2. Navigate to your Tutorial 3 folder, then to the subfolder containing your FOXP2 sequences:

   ```sh
   cd tutorial_3/ncbi_dataset/data/
   ```

3. Copy your sequence files (`cds.fna`, `cds_headers.fna`, `rna.fna`, and `protein.faa`) from the Tutorial 3 folder to the Tutorial 4 folder:

   ```sh
   cp cds.fna cds_headers.fna protein.faa rna.fna ../../../tutorial_4/
   ```

4. Navigate to your Tutorial 4 folder and list its contents to check that the files were copied:

   ```sh
   cd ../../../tutorial_4
   ls
   ```

You should now see your sequence files in the folder.

5. **Awarnach users only:** Activate the conda environment where MAFFT is installed. MAFFT will not be available until you activate it.

   ```sh
   source activate mafft
   ```

6. Run MAFFT using a command with this format:

   ```sh
   mafft [options] input.fasta > output.fasta
   ```

   🐞 **Let's break down the command:**

   * `[options]` are the MAFFT settings you can choose. See the [MAFFT manual](https://mafft.cbrc.jp/alignment/software/manual/manual.html) for the full list.
   * `input.fasta` is the name or path to your unaligned sequence file.
   * `output.fasta` is the name or path for the output alignment.

   Here's an example command:

   ```sh
   mafft --nuc --globalpair --maxiterate 1000 --inputorder cds.fna > FOXP2_nuc_aligned_mafft.fasta
   ```

   `cds.fna` is the **unaligned** sequence file downloaded from NCBI. `FOXP2_nuc_aligned_mafft.fasta` is an example output name; you can choose another name, but keep the `.fasta` extension.

🐞 **Want to build your own command?**

1. Read the [MAFFT manual](https://mafft.cbrc.jp/alignment/software/manual/manual.html) to learn what the options in the example command do.
2. Choose your own options, as you did for the online version, and build a MAFFT command.
3. Run your command in the terminal and watch the magic happen!

## 3. Aligning with PRANK

### 🍄 Using PRANK on command line

1. In your terminal, make sure you are logged in to your lab's server.
2. Activate the PRANK environment:

   ```sh
   source activate prank
   ```

3. Run PRANK with a command like this, replacing the input and output names with your own:

   ```sh
   prank -d=input.fasta -o=output -F
   ```

   🐞 **Let's break down this command:**

   * `-d` specifies the input data file.
   * `-o` specifies the output name or path.
   * `-F` is an option recommended by the manual to avoid ignoring gaps and insertions.

4. View the resulting alignment in the terminal using `cat` and the output file name.

## 4. Visualizing alignments

There are many programs for viewing and editing multi-species alignments. You can find a list of alignment viewers [here](https://en.wikipedia.org/wiki/List_of_alignment_visualization_software).

Many alignment viewers have similar options, so feel free to choose the one that best suits your preferences. 🌸
My favourite is [AliView](https://ormbunkar.se/aliview/), so this tutorial uses it to view alignments.

### 🍄 Using AliView to visualize alignments

1. Download [AliView](https://ormbunkar.se/aliview/#DOWNLOAD), choosing the download link for your operating system and version.
2. Open AliView, select **File > Open file**, and navigate to the alignment you want to view.

## 5. Editing alignments

### 🍄 Removing stop codons from an alignment

Use `seqkit mutate` to remove the stop codons `TAA`, `TAG`, and `TGA` from an alignment:

```sh
seqkit mutate -i -p "TAA|TAG|TGA" -r "" alignment.fasta > alignment_no_stops.fasta
```