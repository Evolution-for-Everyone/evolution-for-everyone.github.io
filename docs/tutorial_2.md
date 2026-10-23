## Learning goals
* [Server? What is that?](https://github.com/Evolution-for-Everyone/bioinformatics-for-everyone/wiki/Tutorial-2:-Working-on-a-server#1-server-what-is-that)
* [Accessing a server](https://github.com/Evolution-for-Everyone/bioinformatics-for-everyone/wiki/Tutorial-2:-Working-on-a-server#2-accessing-a-server)
* [The Alliance servers](https://github.com/Evolution-for-Everyone/bioinformatics-for-everyone/wiki/Tutorial-2:-Working-on-a-server#-the-alliance-servers)
* [The Awarnach server](https://github.com/Evolution-for-Everyone/bioinformatics-for-everyone/wiki/Tutorial-2:-Working-on-a-server#-the-awarnach-server)
* [Transferring files between the server and your computer](https://github.com/Evolution-for-Everyone/bioinformatics-for-everyone/wiki/Tutorial-2:-Working-on-a-server#3-transferring-files-between-the-server-and-your-computer)
* [Transferring files via command line](https://github.com/Evolution-for-Everyone/bioinformatics-for-everyone/wiki/Tutorial-2:-Working-on-a-server#-transferring-files-via-command-line)
* [Transferring files with Filezilla](https://github.com/Evolution-for-Everyone/bioinformatics-for-everyone/wiki/Tutorial-2:-Working-on-a-server#-transferring-files-with-filezilla)

## 1. Server? What is that?

If you are in a bioinformatics lab, you will probably have to work on a server at some point. When I first joined a lab back in my undergrad years, _server_ was this ethereal, mysterious word to describe a parallel universe that I could access from my computer to run some analysis. Back then, I had so many unanswered questions:

* What is a server? 
* How does it look like?
* What is it made of?
* Where does it stay?
* Why do we need them?

Let's start this tutorial by answering those questions:

### 🍄 What is a server?
A server is a supercomputer or a collection of computers working together, sitting in a room somewhere. The reason why we need servers is the same as why we, as humans, get together to solve complex problems - for some kinds of problems, one brain (one computer) is enough, for others, we need a room of people thinking together (server).

A small server can be just a few computers in a research office, but a large server can look like this: \
_This is the Narval server, located at the [École de technologie supérieure](https://www.etsmtl.ca/en/home) in Montreal._

<img src="https://github.com/user-attachments/assets/1c1643d0-97d3-4352-a64a-62d15ed624fe" width="500">

### 🍄 What's cool about a server?
* servers are way larger and more powerful than our personal computers, so they can store more data, process things faster and deal with more complicated problems
* it allows you to run a lot of different software outside your own laptop, using the combined power of this collection of computers (even heavy analyses that your laptop might not be able to handle!).
* when you run something on a server (like a code, an analysis or a software) it will keep running even after you shut down your laptop/personal computer!
* you don't have to worry about installing all the software for your research project and keeping them updated - our server administrator will do that for you!

_**That sounds awesome! How do I enter the magic world of the server?**_ <br>
Let's learn more about that in the next section ⬇️

## 2. Accessing a server

Our laptops/computers can connect to a server via internet, and for that we just need to use the `ssh` (secure shell) command on our terminal! <br>
The `ssh` command allows you to log in to any server, as long as you have these 4 pieces of information:
* server
* username
* password
* port

..and using the following command: `ssh -p port username@server` <br>
After you type that command, the prompt will ask you for a password, as we'll see in the examples below. <br>

### 🍄 The Alliance servers
The Digital Research Alliance of Canada has a collection of servers available to any researcher affiliated with a Canadian institution: \
[Beluga](https://docs.alliancecan.ca/wiki/B%c3%a9luga/en), [Cedar](https://docs.alliancecan.ca/wiki/Cedar), [Graham](https://docs.alliancecan.ca/wiki/Graham), [Narval](https://docs.alliancecan.ca/wiki/Narval/en#Node_characteristics) and [Niagara](https://docs.alliancecan.ca/wiki/Niagara)

🐞 **Registering for a server account with the Alliance** \
To get access to the Alliance's servers, first you need to create an account by [registering](https://alliancecan.ca/en/services/advanced-research-computing/account-management/apply-account) with the Alliance CCDB 
* if you are a PI, you can apply directly for an account 
* if you are a student/member of a research group, your supervisor needs have an account first, so they can sponsor your application at no cost.

🐞 **Setting up your server account** \
Once your application has been approved (usually takes 1-2 business days), and before you can use the server, you need to set up:
1. [Multi-factor Authentication](https://docs.alliancecan.ca/wiki/Multifactor_authentication)
2. [SSH-keys](https://docs.alliancecan.ca/wiki/SSH_Keys) (recommended) 
3. and for Niagara, you need to access the [opt-in page](https://ccdb.alliancecan.ca/services/opt_in) and click on the join button. In the future, this step will be required for other servers as well.

🐞 **Logging into your account** \
Now, you can use the `ssh` command to log in to your server account! Just type the following command on the terminal:

```bash
ssh [username]@[server].alliancecan.ca
```
replacing `[username]` with your username and `[server]` with the name of the server you wish to log in to.

### 🍄 The Awarnach server

The Bielawski Group's server is called Awarnach (there's a cool story behind that name, read more [here](https://awarnach.mathstat.dal.ca/dokuwiki/doku.php?id=awarnach:home)). It's a cluster server - which means it's a bunch of computers working together - that stays inside Joe's office, centralizing all the data, information and software for our lab's research projects. 

To log in on our server, we will:
1. Open the terminal
2. Use the `ssh` command replacing the port, user name and server name with the proper information. <br>
- Our server's name is: `awarnach.mathstat.dal.ca`, the port is `22` and each one of us has our own username. <br>
Here's how the full command looks like, after I added my own user name `leticiamagpali` (replace that with yours!):

```
ssh -p 22 leticiamagpali@awarnach.mathstat.dal.ca
```
📍**Note**: Your username and password are set up by the server's administrator (ask your supervisor to arrange that and get the admin's contact for troubleshooting)

**🍄 Let's practice!** <br>
Log in to Awarnach using the `ssh` command, and the username and password that were sent to you. <br>
_When you type in your password, nothing will show on the screen_, so just type the full password one time and hit enter. <br> 
After successful log in, your screen should look like this: <br>

![Screenshot 2024-05-23 at 4 58 15 PM](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/7f9e71e6-3c99-416f-a805-90d0b376de62)

**Ok, now that I'm logged in, what if I want to exit the server?** <br>
That's simple! Just type `exit` on the prompt, and hit enter! <br>
There will be a message to confirm you actually left the server, like this:
```
logout
Connection to awarnach.mathstat.dal.ca closed.
```
**What if I want to change my password?** <br>
You can change your server password at anytime entering the command `passwd` on the terminal prompt. <br>
It will ask you first to type the current password, then the new one. <br>

> [!WARNING]
>None of these passwords will show when you type them, so make sure to just type one time and press enter!

## 3. Transferring files between the server and your computer

When you are working on server, all the information and files you produce will be stored on the server - not on your personal computer. So anytime you want to look at your results on your computer using your programs, you will need to transfer them from the server first. <br>
There are two ways of doing that: via command line or using a software with a graphic interface (in our case, **Filezilla**). 

Let's look at both of them below:

### 🍄 Transferring files via command line

We can use the `scp` command on the terminal to transfer/copy files from the server to our computer and vice-versa. <br>
For that, follow the steps below:

1. Open a terminal session _on your computer_
2. Now let's test the scp command on two different cases: <br> 
In each case, copy the command and edit it, replacing the place holders with the actual paths in your local and remote. 

* **Transferring from remote (server) to local (your computer)** 
```
scp [username]@[server]:/path/to/remote/file /path/to/local/destination/folder
```

* **Transferring from local (your computer) to remote (server)** 
```
scp /path/to/local/file [username]@[server]:/path/to/remote/destination/folder
```

> [!TIP]
> you can use `pwd` at the server and the destination folder to find out the full path!

**Transferring from to local (your computer) to remote (server)**
1. Open a terminal session 
3. Now go to your destination folder on your computer and use `ls` to check if your file transfer was successful 🌸

### 🍄 Transferring files with Filezilla

Filezilla is a software you can download to your computer, that allows you to manually transfer files from the server to your computer using drag and drop and clickable options. This can be very useful when you have a lot of stuff to transfer and you are not feeling like writing code. <br>
Let's get started:

1. Download [Filezilla](https://filezilla-project.org/) by clicking on `Quick download links > Download Filezilla Client` 
2. Open Filezilla on your applications, and type on the top bar: the server's name (host), your username, password, and server port (go back to the [Awarnach](https://github.com/leticiamagpali/vocal-learning-project/wiki/Tutorial-2:-Working-on-a-server#-the-awarnach-server) session of this tutorial to find our server's login info)
3. Then, click on `Quick connect` and you should see your server's folders show on right side of your screen, like this: 

<img src="https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/99941072-66f3-469a-8924-4e82b29d9fec" width="800">

4. Then, you can just drag and drop files from the left side of your screen (your computer) to the right side (your folders), and navigate through folders on both sides. **SOOO MUCH POWER!!**

## 4. Challenge - transfering your master folder to the server
Remember the master folder you created on Tutorial 1 (`tutorials`)? Your task now is to transfer a copy of this folder to your server home folder! You can use `scp` or Filezilla, whichever one you prefer! <br>
You got this!

<details>

<summary>After you try, click here to see a step-by step guide of how I do it.</summary>

- To do scp, I usually have 2 terminal windows open: in one window, I am connected to my personal computer (letixa@eugenio) and on the other window, I am logged into my server account (leticiamagpali@awarnach.mathstat.dal.ca). This makes it easier to copy and paste information from one to the other!

- Now, to copy the tutorials folder from my computer to the server, I need two things:
    * the path to the folder on my computer
    * the path to the destination on the server (where I want this folder to be copied to)

* To find the destination path, I will go to my **server window** and navigate to the destination folder I chose:
```bash
cd bioinfo4everyone/
```
Once I am inside the destination folder, I can find out its path using the pwd command:
```bash
leticiamagpali@awarnach:~/bioinfo4everyone$ pwd
/home/leticiamagpali/bioinfo4everyone 
```
The path to my folder is /home/leticiamagpali/bioinfo4everyone, I will select it and copy it with Ctrl+C.

* On my **computer window** I will go to the place where the tutorials folder is located. If you followed Tutorial 1 and created your tutorials folder in the Documents, you should use:
```
cd Documents
```
In my case, my tutorials folder is inside my Google Drive, so my cd command is a little longer:
```bash
cd Google\ Drive/My\ Drive/evolution4everyone/bioinformatics-for-everyone/solved_tutorials/
```
Once you are inside tutorials, you can type the scp command: 
```bash
scp /path/to/local/file [username]@[server]:/path/to/remote/destination/folder
```
replacing /path/to/local/file with tutorials, [username] and [server] with your login information and /path/to/remote/destination/folder with the path you copied above. So in my case it will look like this:

```bash
scp tutorials leticiamagpali@awarnach.mathstat.dal.ca:/home/leticiamagpali/bioinfo4everyone
```

</details>
