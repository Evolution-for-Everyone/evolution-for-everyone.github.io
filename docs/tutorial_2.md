# Tutorial 2 - Working on a server

## 1. Server? What is that?

If you are in a bioinformatics lab, you will probably have to work on a server at some point. When I first joined a lab as an undergraduate, _server_ was this ethereal, mysterious word for a parallel universe I could access from my computer to run analyses. Back then, I had so many unanswered questions:

* What is a server?
* How does it look like?
* What is it made of?
* Where does it stay?
* Why do we need them?

Let's start this tutorial by answering those questions:

### 🍄 What is a server?

A server is a computer, or a collection of computers working together, that provides resources such as processing power, storage, or software. We use servers for the same reason people work together to solve complex problems: one computer may be enough for some tasks, while others need more computing power.

A small server can be just a few computers in a research office, while a large server can look like this:

![Narval server at the École de technologie supérieure in Montreal](https://github.com/user-attachments/assets/1c1643d0-97d3-4352-a64a-62d15ed624fe){ width="500" }

### 🍄 What's cool about a server?

* Servers are often more powerful than personal computers, so they can store more data, process it faster, and handle more complicated problems.
* You can run software on a server using its computing resources, including analyses that your laptop might not be able to handle.
* A process running on a server can continue after you disconnect from it, if it was started in a way that keeps it running.
* A server administrator may install and maintain software for the research group.

_**That sounds awesome! How do I access a server?**_

Let's learn more in the next section.

## 2. Accessing a server

Our computers can connect to a server over the internet using the `ssh` (Secure Shell) command in a terminal.
To connect, you need the server's address and your username. Depending on how the server is configured, you may also need a port number, a password, an SSH key, or multi-factor authentication.

The general command is:

```sh
ssh -p [port] [username]@[server]
```

The `-p [port]` part is only needed if the server uses a non-default SSH port. After you enter the command, you may be asked to authenticate.

### 🍄 The Alliance servers

The Digital Research Alliance of Canada has a collection of servers available to researchers affiliated with Canadian institutions: [Beluga](https://docs.alliancecan.ca/wiki/B%C3%A9luga/en), [Cedar](https://docs.alliancecan.ca/wiki/Cedar), [Graham](https://docs.alliancecan.ca/wiki/Graham), [Narval](https://docs.alliancecan.ca/wiki/Narval/en#Node_characteristics), and [Niagara](https://docs.alliancecan.ca/wiki/Niagara).

🐞 **Registering for an Alliance server account**

To access the Alliance servers, first [register for an account](https://alliancecan.ca/en/services/advanced-research-computing/account-management/apply-account) with the Alliance's CCDB.

* If you are a principal investigator (PI), you can apply directly for an account.
* If you are a student or research-group member, your supervisor must have an account to sponsor your application at no cost.

🐞 **Setting up your server account**

Once your application has been approved (usually within 1–2 business days), follow the setup instructions for:

1. [Multi-factor authentication](https://docs.alliancecan.ca/wiki/Multifactor_authentication)
2. [SSH keys](https://docs.alliancecan.ca/wiki/SSH_Keys) (recommended)
3. For Niagara, the [opt-in page](https://ccdb.alliancecan.ca/services/opt_in). Open the page and click the join button. Check the Alliance documentation for current requirements for other servers.

🐞 **Logging in to your account**

Use the login command provided by the Alliance for your selected server. For example:

```
ssh [username]@[server].alliancecan.ca
```

Replace `[username]` and `[server]` with your account and server details. The exact login method may differ depending on the server's authentication requirements.

### 🍄 The Awarnach server

The Bielawski Group's server is called Awarnach. [Read the story behind its name](https://awarnach.mathstat.dal.ca/dokuwiki/doku.php?id=awarnach:home). It is a cluster—a group of computers working together—located in Joe's office. It centralizes data, information, and software for the lab's research projects.

To log in:

1. Open a terminal.
2. Run the `ssh` command with the server's address and your username. The server address is `awarnach.mathstat.dal.ca`, the port is `22`, and each user has a unique username.

For example, if your username is `leticiamagpali`, the command is:

```sh
ssh -p 22 leticiamagpali@awarnach.mathstat.dal.ca
```

📍 **Note:** The server administrator sets up your account. Ask your supervisor how to get access and who to contact for troubleshooting.

**🍄 Let's practice!**

Log in to Awarnach using the `ssh` command and the account details provided to you.
When you type a password, nothing appears on the screen. Type it once, then press Enter.

After a successful login, your screen should look like this:

![Terminal after logging in to Awarnach](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/7f9e71e6-3c99-416f-a805-90d0b376de62)

**How do I exit the server?**

Type `exit` at the prompt and press Enter. You should see a message confirming that you disconnected:

```
logout
Connection to awarnach.mathstat.dal.ca closed.
```

**How do I change my password?**

If password changes are enabled on your server, run `passwd` at the terminal prompt. It will ask for your current password and then your new password.

!!! warning
    Passwords do not appear on the screen while you type them. Enter each password once, then press Enter.

## 3. Transferring files between the server and your computer

When you work on a server, the files you create are stored on the server, not on your personal computer. To use those files with programs on your computer, you may need to transfer them first.

You can transfer files using the command line or a graphical application such as **FileZilla**.

### 🍄 Transferring files via command line

Use the `scp` command in a terminal on your computer to copy files between your computer and the server.

1. Open a terminal on your computer.
2. Choose the command for the direction you want to copy, replacing the placeholders with the correct paths and account details.

**From the server to your computer**

```sh
scp [username]@[server]:/path/to/remote/file /path/to/local/destination/
```

**From your computer to the server**

```sh
scp /path/to/local/file [username]@[server]:/path/to/remote/destination/
```

To copy a directory and everything inside it, add the `-r` option after `scp`. For example:

```sh
scp -r tutorials [username]@[server]:/path/to/remote/destination/
```

!!! tip
    Use `pwd` to find the current directory's full path. Run it on the server for a remote path, or in a terminal on your computer for a local path.

### 🍄 Transferring files with FileZilla

FileZilla is an application that lets you transfer files between your computer and a server using a graphical interface. It can be useful when you want to drag and drop files instead of entering commands.

1. Download [FileZilla Client](https://filezilla-project.org/).
2. Open FileZilla and enter the server host, username, password or other authentication details, and port. For Awarnach's details, see [The Awarnach server](#the-awarnach-server).
3. Click **Quickconnect**. Your server's folders should appear on the right side of the window.

    ![FileZilla showing local and server folders](https://github.com/leticiamagpali/vocal-learning-project/assets/71052306/99941072-66f3-469a-8924-4e82b29d9fec){ width="800" }

4. Drag and drop files from the left side (your computer) to the right side (the server). You can navigate through folders on both sides.

## 4. Challenge: transferring your master folder to the server

Remember the master folder you created in Tutorial 1 (`tutorials`)? Your task is to transfer a copy of it to your home folder on the server. Use `scp` or FileZilla—whichever you prefer!

??? note "After you try, open this step-by-step guide"

    To use `scp`, I usually have two terminal windows open: one for commands on my computer and one connected to the server. This makes it easier to look up and copy paths.

    To copy the `tutorials` folder from my computer to the server, I need:

    * The path to the folder on my computer.
    * The destination path on the server.

    To find the destination path, go to the chosen folder in the **server terminal** and run `pwd`:

    ```sh
    cd bioinfo4everyone
    pwd
    ```

    In this example, the path is `/home/leticiamagpali/bioinfo4everyone`.

    On your **computer**, navigate to the directory that contains the `tutorials` folder. If you created it in Documents, run:

    ```sh
    cd ~/Documents
    ```

    Then copy the folder to the server, replacing the username and destination path with your own:

    ```sh
    scp -r tutorials [username]@awarnach.mathstat.dal.ca:/home/[username]/bioinfo4everyone/
    ```
