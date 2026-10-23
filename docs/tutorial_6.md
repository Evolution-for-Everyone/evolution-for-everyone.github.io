## 🌺 What are evolutionary models?

In the previous tutorials, we learned how to:

* Extract genomic sequences from online databases.
* Make sequence alignments.
* Estimate gene trees.

Now, we are going to use our sequence alignments and gene trees as input for an evolutionary model using a program called codeml.

!!! important "What is a model?"
    **A model is a representation of a process**—in our case, the evolutionary process. Codeml models are mathematical representations of how genomic sequences evolve.

### 🍂 Why are evolutionary models important?

We use evolutionary models to ask questions and test hypotheses about how a genomic sequence changed through time. For example:

* Did brain genes evolve differently in humans than in other animals?
* Which genes are evolving faster in our genome?
* Which genes or non-coding sequences are associated with adaptations in marine mammals?

## 🌺 How do we measure evolution on a sequence?

There are many ways to represent evolution mathematically in a model. In molecular evolution (the study of genes, proteins, and related molecules), one popular measure is the **omega ratio**, or *ω*.

!!! important "The omega ratio"
    **ω** measures natural selection acting on a sequence. It indicates the relative rates of nonsynonymous and synonymous substitutions, and is used to infer patterns of selection.

See the infographic below for a brief explanation of the **ω ratio**, and read [these slides](https://drive.google.com/file/d/1ncnQr0jN3sovM9SUYjGnSPND9xjAoe4N/view?usp=sharing) for more details.

![Screenshot 2024-07-17 at 10 36 19 PM](https://github.com/user-attachments/assets/ca800bb4-6c67-457c-8222-27b043c4797f)

## 🌺 What is codeml?

* **Codeml** is a program for running evolutionary models, particularly models of codon and amino acid substitution.
* Codeml models use the **ω ratio** to estimate how codon or protein sequences changed through time and across different lineages.

### 🍂 What can we do with codeml?

We can use codeml for two main purposes: hypothesis testing and model fitting.

* **Hypothesis testing:** We compare an alternative hypothesis (a possible explanation for patterns in the data) with a null hypothesis (a model without the proposed effect). Codeml can help us test whether the data provide evidence against the null hypothesis.
* **Model fitting:** We use the sequences and trees to estimate parameters and learn about the evolutionary process, without starting from a specific hypothesis.

When results support an alternative hypothesis, codeml can also help identify which parts of a gene may be evolving in a particular way.

!!! tip "Learn more about PAML and codeml"
    Codeml is part of **PAML**, a package that includes other programs. Learn more on the [PAML website](http://abacus.gene.ucl.ac.uk/software/paml.html) or in the [PAML manual](http://abacus.gene.ucl.ac.uk/software/pamlDOC.pdf).

    Recommended readings, from beginner to advanced:

    * [Beginner's Guide on the Use of PAML to Detect Positive Selection](https://academic.oup.com/mbe/article/40/4/msad041/7140562)
    * [Adaptive Molecular Evolution: Detection Methods](http://awarnach.mathstat.dal.ca/~joeb/PAML_lab/resources/00171.PUBLISHED.pdf)
    * [Detecting the Signatures of Adaptive Evolution in Protein-Coding Genes](https://drive.google.com/file/d/1QYjR8H_bx5qI_9T0sdX-jId0VU1NRqt2/view?usp=sharing)
    * [Inference of Episodic Changes in Natural Selection Acting on Protein Coding Sequences via CODEML](https://drive.google.com/file/d/1F9_Ig2p5dEE6MLiLWp5hPxxHIrrCgRZh/view?usp=sharing)

### 🍂 What types of models does codeml have?
Codeml has three types of models: branch models, site models and branch-site models.

* **Branch models** allow ω to vary among branches. They can test whether some lineages in a phylogenetic tree evolved differently from others.

    _For example: I wonder if whales evolved differently from other mammals._

* **Site models** allow ω to vary among codons (sites). They can test whether some sites in a sequence evolved differently from the rest, or under positive selection.

    _For example: Which codons in this virus genome are evolving faster, and could that help explain how the virus is adapting to a vaccine?_

* **Branch-site models** allow ω to vary among both branches and sites. They can test whether particular sites on specific branches evolved differently, or under positive selection.

    _For example: I found evidence that whales evolved differently from other mammals. Which sites in these whale genes evolved faster?_


## 🌺 Running codeml on command-line

Before we begin, log in to your lab server. See [Tutorial 2](tutorial_2.md) for instructions.
To run codeml, we first need a codon alignment and a codon tree.

### 🍂 Creating a codon alignment

To generate a codon alignment, we will use PRANK to process the **FOXP2 nucleotide alignment** created with MAFFT in [Tutorial 4](tutorial_4.md).

1. Activate the PRANK environment:

    ```sh
    source activate prank
    ```

2. Run PRANK using this command, replacing the input and output names with your own:

    ```sh
    prank -d=input.fasta -o=output_name -codon -F
    ```

    Replace `input.fasta` with the name or path to your nucleotide alignment, and replace `output_name` with the name you want for the output file. No extension is needed.

    For example:

    ```sh
    prank -d=FOXP2_nuc_aligned.fasta -o=FOXP2_codon_aligned -codon -F
    ```

#### Converting the alignment format

Codeml requires an alignment in PAML format, which is a modified PHYLIP format. To convert your codon alignment, use PRANK with the `-convert` option:

```sh
prank -convert -d=alignment_codon.fas -f=paml -o=output_file_name -keep
```

### 🍂 Creating a codon tree

Now that we have a codon alignment, we can use IQ-TREE to generate a codon tree on the server.

1. Activate the IQ-TREE environment:

    ```sh
    source activate iqtree
    ```

2. Run IQ-TREE, replacing the alignment name and output prefix with your own. For the sequence type (`-st`), use `CODON`:

    ```sh
    iqtree -s sequence_alignment -st CODON -m MFP -pre output_file_prefix -nt AUTO
    ```

For more details about running IQ-TREE, see [Tutorial 5](tutorial_5.md).

### 🍂 Preparing your input files

!!! warning "Use codon input files"
    You must use a codon alignment and a codon tree. Codeml will not run with a DNA or protein alignment.

1. Create a master folder for your codeml analyses. You can name it something other than `codeml` if you prefer:

    ```sh
    mkdir codeml
    ```

2. Create a folder for this codeml run. We will start with model M0:

    ```sh
    mkdir codeml_M0
    ```

3. Find the **codon alignment** and **codon tree** for the FOXP2 gene on your server.

4. Use `mv` to move the alignment and tree files into your `codeml_M0` folder. Replace the placeholders with your file paths:

    ```sh
    mv path/to/file/to/move path/to/destination
    ```

### 🍂 Writing the control file

We're almost there! Now we need to write the codeml control file. 😄

!!! tip "What is the control file?"
    The control file is a text document where you specify options for codeml. It tells codeml which model to run, where to find the input files, where to write the output, and which parameters to use.

The codeml control file looks like this:

```text
seqfile = Mx_aln.phy                    * Path to the alignment file
treefile = Mx_unroot.tree               * Path to the tree file
outfile = out_M0.txt                    * Path to the output file
noisy = 3                               * Display moderate information on the screen
verbose = 1                             * Detailed output file
seqtype = 1                             * Codon data
ndata = 1                               * One gene alignment
icode = 0                               * Universal genetic code
cleandata = 0                           * Do not remove sites with ambiguity data
model = 0                               * One ω for all branches (M0 and site models)
NSsites = 0                             * One ω for all sites (M0 and branch model)
CodonFreq = 2                           * Use F3x4 model
clock = 0                               * Assume no clock
fix_omega = 0                           * Enables option to estimate omega
omega = 0.5                             * Initial omega value
```

Each line contains a codeml option, its value, and a comment after `*`. Codeml ignores the comments; they explain what the options mean.

The control file has many options, but you can think of them as settings for fine-tuning the model. In this tutorial, we will focus on six options:

#### 🍁 Essential options for codeml beginners

1. `seqfile` — the name or path to your codon alignment.
2. `treefile` — the name or path to your codon tree.
3. `outfile` — the name for your codeml output file.
4. `model` — the branch model to run.
5. `NSsites` — the site model to run.
6. `omega` — the initial omega value.

Now let's configure the control file for model M0 by setting these options.

#### 🍁 Setting up the control file for the M0 model

**1. What is the M0 model?**

* The **M0 model** is a basic codeml model, often used as a null hypothesis or to explore a data set.
* M0 is also called the "one-ratio" model because it estimates **one ω ratio across all branches and sites** in the phylogenetic tree. It assumes that all lineages and codons evolve at the same rate.
* This assumption may be too simple for some data sets. However, models are simplified representations of real-world processes, and M0 may fit some data well.
* M0 can serve as a **null hypothesis** for comparison with more complex models.
* Its estimated ω provides a baseline summary across sites and lineages.

**2. Set up the M0 control file**

To specify the M0 model, write the following options in your control file:

```text
seqfile = name_sequence.phy             * Name or path to the alignment file
treefile = name_tree.tree               * Name or path to the tree file
outfile = out_M0.txt                    * Name or path to the output file
model = 0                               * One ω for all branches (M0 and site models)
NSsites = 0                             * One ω for all sites (M0 and branch model)
omega = 0.5                             * Initial omega value
```

### 🍂 Running codeml

1. Activate the PAML environment:

    ```sh
    source activate paml
    ```

2. Run codeml, replacing `control_file.ctl` with the name of your control file:

    ```sh
    codeml control_file.ctl
    ```
