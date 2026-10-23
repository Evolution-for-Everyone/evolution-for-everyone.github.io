## 🌺 What are gene trees? { #gene-trees }

Gene trees, like other phylogenetic trees, represent a hypothesis about the evolutionary history of a group of organisms.
While species trees may be inferred using many genes and other evidence, **a gene tree is inferred from an alignment of one gene**.

!!! tip "Gene trees and species trees"
    A gene tree represents the evolutionary history of a particular gene. It may therefore differ from a species tree, which represents the evolutionary history of the species.

📍 Similarly, we can use a protein alignment to make a protein tree, or a codon alignment to make a codon tree.

### 🍄 IQ-TREE: a program to estimate phylogenetic trees { #iqtree }

One popular program for estimating phylogenetic trees is [IQ-TREE](http://www.iqtree.org/).

IQ-TREE can estimate gene, protein, and codon trees. These trees can help us understand the evolutionary history represented by a sequence alignment and can be used as input for evolutionary models.

📍 IQ-TREE has both a web version and a command-line version. Let's learn how to use both.

## 🌺 Using IQ-TREE web version { #iqtree-web }

1. Open the [IQ-TREE web server](http://iqtree.cibiv.univie.ac.at/).
2. Read the [IQ-TREE web server tutorial](http://www.iqtree.org/doc/Web-Server-Tutorial).
3. Use **Browse** to select your **sequence alignment** file.
4. Choose your analysis options:

    * Under **Sequence type**, select the type of alignment you have: `DNA` (nucleotides), `codon`, or `protein`.

    ![IQ-TREE sequence type options](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/d593f8d0-19ce-45ef-a558-6ff63e3c7c1c)

    * Under **Substitution model**, leave the default `Auto` option to let IQ-TREE select a suitable substitution model for your data.

    ![IQ-TREE substitution model options](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/4d434787-df01-4d58-b100-f52aa65c21bf)

    * Under **Branch Support Model**, select `None` for bootstrap analysis and `No` for the SH-aLRT branch test. These tests provide statistical support for the tree topology; if you only want to inspect the topology, you can leave them off.

    ![IQ-TREE branch support options](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/37e356cd-f622-4318-baad-aee479e00283)

5. Optionally, enter your email address if you would like to receive a notification, then select **Submit**.
6. Open the **Analysis Results** tab to check the status of your job. When the status is **Success**, select the checkbox beside the job and choose **Download selected jobs**.

## 🌺 Using IQ-TREE on the command line { #iqtree-cli }

1. Access your lab server. See [Tutorial 2](tutorial_2.md) for instructions.
2. Navigate to the folder containing your sequence alignments. You can use nucleotide, protein, or codon alignments as input.
3. Activate the IQ-TREE environment:

    ```sh
    source activate iqtree
    ```

4. Run IQ-TREE with a command like this, replacing the placeholders with settings for your data:

    ```sh
    iqtree -s sequence_alignment -st sequence_type -m model -pre output_file_prefix -nt number_threads
    ```

    The options are:

    * `-s` specifies the path to your sequence alignment.
    * `-st` specifies the sequence type: `DNA`, `AA`, or `CODON`.
    * `-m` selects the model IQ-TREE uses to estimate the tree. To let IQ-TREE select a model, use `-m TEST` or `-m MFP`.
    * `-pre` sets the prefix for the output files. You do not need to specify a file extension because IQ-TREE creates several output files with different extensions.
    * `-nt` specifies the number of CPU cores to use. You can use `-nt AUTO` to let IQ-TREE choose a number of cores.

    Here is an example command:

    ```sh
    iqtree -s FOXP2_nuc_aligned.fasta -st DNA -m MFP -pre FOXP2 -nt AUTO
    ```

    📍 For more information about command-line options, see the [IQ-TREE command reference](http://www.iqtree.org/doc/Command-Reference).

5. After IQ-TREE finishes, list the output files with `ls FOXP2*`. This lists files whose names start with `FOXP2`.
6. Find the file ending in `.treefile` and download it to your computer using `scp` or FileZilla. **This is the main result: it contains the phylogenetic tree estimated by IQ-TREE.**

📍 Now let's look at your tree.

## 🌺 Visualizing IQ-TREE gene trees { #visualize-trees }

The main output of IQ-TREE is a tree file in **Newick** format. What does that mean? Let's find out!

1. View your `.treefile` in the terminal with `cat FOXP2.treefile`. You should see something like this:

    ```text
    (NM_212435.1_323-2467:0.0646339334,((NM_014491.4_557-2704:0.0025344249,XM_054687043.2_337-2613:0.0014022172):0.0196793068,(((NM_001205569.3_1-2238:0.0189337982,(XM_019925131.2_314-2584:0.0053703994,XM_036862984.1_730-2931:0.0083157654):0.0130501620):0.0061924234,XM_038439870.1_389-2602:0.0329259681):0.0027640605,XM_023760067.1_254-2446:0.0485376216):0.0026152117):0.0056417332,(XM_004382567.2_1-2250:0.0225517894,XM_023544567.1_404-2617:0.0163154299):0.0081864833);
    ```

2. To view the tree graphically, download [FigTree](http://tree.bio.ed.ac.uk/software/figtree/) to your computer.

3. Open FigTree, select **File > Open**, and choose your tree file (for example, `FOXP2.treefile`). The Newick tree will load, and you should see something like this:

    ![FOXP2 tree open in FigTree](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/d9d3c394-5fe5-404c-af72-67b4e7917ce5)

4. FigTree has a menu on the left with several options:

    * Expand **Tip labels** to change the font and size of the names at the tips of the tree.
    * Use **Appearance** to change the branch width.
    * The top menu includes options to change branch and node colors and rename tip labels.

📍 Explore FigTree and customize your tree. Try these tasks:

* Adjust the tree layout using the options in **Tree Layout**.
* Make the branches thicker using **Appearance > Line Weight**.
* Change the color of three branches. Under **Selection Mode**, select **Clade**, choose a branch, then select **Colour** and choose a color.
* Rename species labels. Under **Selection Mode**, select **Taxa**, choose a tip, then select **Annotate** and enter a new name.

When you are done, select **File > Export PNG**.
