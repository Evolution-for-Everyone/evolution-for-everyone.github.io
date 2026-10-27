# Tutorial 1 - Setting up your workspace

Before you get started in the fantastical world of bioinformatics and molecular evolution, there's a few programs your computer needs first.
We are going to install those one by one.

Some of the programs we will install are the regular kind of download that we are all used to, but others require the **command-line**, which you have already learned about in [Tutorial 0](tutorial_0.md).

## Installing X-code (for mac users)
Xcode is Apple's official Integrated Development Environment (IDE) for macOS used to build, test, debug, and submit software.
You can install it directly from the [macOS Apple store](https://apps.apple.com/us/app/xcode/id497799835?mt=12)

## Installing alignment visualizing tools
In Tutorial 3, we will visualize sequence alignments.   
Below are the links to the most commonly used free apps for alignment visualization:    

- [Aliview](https://ormbunkar.se/aliview/#DOWNLOAD)
- [Jalview](https://www.jalview.org/download/)
- [Seaview](https://doua.prabi.fr/software/seaview)

Our tutorial follows Aliview, but you're welcome to try them all, and choose your preferred one!


## Installing Conda

Conda is an environment and software manager. It is required to install and run NCBI datasets, which you will do next.   
[Install conda here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html#regular-installation). Don't forget to follow the right instructions for your operational system!


!!!success "Checkpoint"
    For the next steps, open up your **terminal app** (it's the black window app, you learned about it in [Tutorial 0](tutorial_0.md).)

## Command-line installation - instructions
As we saw on [Tutorial 0](tutorial_0.md), command-line is a way to talk to your computer using written commands inside an app called terminal. The next software we will install don't have a graphic interface, so we need to download them using the command-line.   

For each software installation, you will do the same actions, described below:

With your terminal open on one side of the screen, and this tutorial on the other:

- Locate the command you need to copy from the tutorial. **Commands are always inside a grey text box**.
- Select the entire command (everything inside the grey box) and copy it.
- Paste the copied command in your terminal prompt.
- Hit Enter; this will runt the command.

!!!danger "Important"
    The terminal will be full of scrolling text for a few seconds/minutes. That's ok! Just leave it there, and **don't type anything else until you see the prompt is accepting commands again**.          
    
    _Remember: how do we know the prompt is accepting commands_?    
    It will show an empty line that has only your user and computer name, like this: 
    ```sh
    user@computer ~ %
    ```

- Once an installation is complete, you can begin another the same way.


## Installing NCBI datasets 

- Create conda environment: `conda create -n ncbi_datasets` 

- Activate conda environment: `conda activate ncbi_datasets`

- Install the datasets conda package: `conda install -c conda-forge ncbi-datasets-cli`



## Installing molecular evolution software 

### MAFFT

1. macOS users

    ```sh
    brew install mafft
    ```

2. Windows/Linux users

    ```sh
    sudo apt update
    sudo apt install mafft
    ```


### IQtree

1. macOS users

    ```sh
    brew install iqtree3
    ```
2. Windows/Linux users
    ```sh
    sudo apt-get update
    sudo apt-get install iqtree
    ```

### PAML    

1. macOS users

    ```sh
    brew install paml
    ```

2. Windows/Linux users

    ```sh
    conda install -c bioconda paml
    ```
