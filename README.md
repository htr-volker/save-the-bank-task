# Save the Bank! Step-by-Step

> Note: Just so it is 100% clear, the following is a fun exercise to teach you how to use Linux VMs in the cloud. You will not actually be preventing a cyber attack!

A group of hackers called *The Collektive* are attempting to launch an attack on Haliwest TSB's central banking servers! It's up to you to infiltrate their systems, gather information about their attack and save the bank!

## Prerequisites

- Log into your QA-provided AWS account
- Spun up a fresh EC2 instance running Ubuntu 20.04 LTS
- SSH into said instance 

## Tutorial

### Hack into the Mainframe! (SSHing into the machine)

1.  First, we need to generate our SSH key pair. To generate a new key pair, run:

    ```bash
    ssh-keygen
    ```

    You can keep the default settings; just hit enter repeatedly until you're told the key pair has been created.

    Two file will be generated in the `.ssh/` folder: `id_rsa` (our private key) and `id_rsa.pub` (our public key).

    In order for our *private key* to authenticate our connection to the hackers' machine, we need to install the *public key* into said machine. Think of the public key as a door lock that can only be opened by the private key.

    Print the contents of the public key to the console using the `cat` command:
    
    ```bash
    cat ~/.ssh/id_rsa.pub
    ```

    Copy the output and paste it to me (Harry) on Teams. I will install the public key onto the hackers' machine for you.

2.  Now we can connect to the hackers' machine via an SSH connection. Run the following in the console:

    ```bash
    ssh <user>@<host>
    ```

    Where:
    - `<user>` should be replaced with the user you'll be logging in as
    - `<host>` should be replaced with the IP address of the machine you're connecting to
    
    I will provide you with both pieces of information – message me if you are unsure.

    If successful, you should see that your terminal input prompt has changed to something like:

    ```bash
    team-1@collektive-team-1:~$
    ```

    ***You're IN!***

### Download ***Cipher*** into the Mainframe! (`git clone` the repo)

1.  We now need to install our decoding software onto the machine so we can decrypt their data.

    Clone [this repository](https://github.com/htr-volker/cipher) to your user's file system with:

    ```bash
    git clone https://github.com/htr-volker/cipher
    ```

    Now, open the folder by running:

    ```bash
    cd cipher
    ```

    Your input prompt should change to something like:

    ```bash
    team-1@collektive-team-1:~/cipher$
    ```

    Use the prompt to know where in the filesystem you are at any given time. The file path in this prompt is referred to as the *current working directory*. You can also enter `pwd` to `p`rint the `w`orking `d`irectory to the console.

2.  Type `ls` into the console and hit enter. You should see the following list of files:

    ```bash
    README.md                 application               cipher-encode             requirements.txt          
    cipher-decode             install.sh                sample_secret_message.txt
    ```

    Use `ls -l` to see more information:

    ```bash
    total 56
    -rw-r--r--  1 team-1  team-1  4198 19 Jul 10:31 README.md
    drwxr-xr-x  8 team-1  team-1   256 18 Jul 22:14 application
    -rwxr-xr-x  1 team-1  team-1    53 17 Jul 19:09 cipher-decode
    -rwxr-xr-x  1 team-1  team-1    53 17 Jul 19:09 cipher-encode
    -rwxr-xr-x  1 team-1  team-1   419 18 Jul 22:29 install.sh
    -rw-r--r--  1 team-1  team-1     8 12 Jul 12:51 requirements.txt
    -rw-r--r--  1 team-1  team-1   300 16 Jul 14:31 sample_secret_message.txt
    ```

    There is a script called `install.sh`. This will install the ***Cipher*** program for you. Run it by entering:
    
    ```bash
    ./install.sh
    ```

3. Let's test that the program is working. To run the program, enter:

    ```bash
    cipher-decode
    ```

    Your terminal window should display something like this:

    ```
    ===========================================================================================

      e88'Y88 ,e,          888                              e88 88e         e88 88e         d88 
     d888  'Y  "  888 88e  888 ee   ,e e,  888,8,          d888 888b       d888 888b       d888 
    C8888     888 888 888b 888 88b d88 88b 888 "    888   C8888 8888D     C8888 8888D     d"888 
     Y888  ,d 888 888 888P 888 888 888   , 888             Y888 888P  d8b  Y888 888P  d8b   888 
      "88,d88 888 888 88"  888 888  "YeeP" 888              "88 88"   Y8P   "88 88"   Y8P   888 
                  888                                                                           
                  888                                                                           

    Loading . . .
    extending light portal . . .                    5.6MB   ✓
    opening public encryptors . . .                 8.0MB   ✓
    unzipping stealthy web . . .                    7.5MB   ✓
    encrypting private webs . . .                   4.7MB   ✓
    playing efficient decryptor . . .               5.8MB   ✓
    playing private 808s . . .                      3.2MB   ✓
    flushing emphatic web . . .                     6.2MB   ✓

    ===========================================================================================
    Enter filename:
    ```

    You'll be prompted to `Enter filename:` – this is the file we're going to decode using ***Cipher***.

    The repo contains an example message for you to decode called `sample_secret_message.txt`.
    
    Type in (or copy/paste) that filename into the prompt and hit enter. Then, just sit back and view the message!

### Infiltrate their Filesystem!

Now we have everything we need to start retrieving the information.

All the data will be found under the user `collecktive`. To log in as that user, enter:

```bash
sudo su - collecktive
```

Breaking down this command:
* `sudo` means "super user do". The "super user" is Linux's equivalent of the administrator user, i.e. the user with the highest privileges. Any command that starts with `sudo` is like when you "Run as Administrator..." on a Windows machine.
* `su` stands for "switch user" and is what allows us to log in as another user on the machine.
* `-` will make sure the current working directory switches to your user's home folder when you log in as them.
* `collecktive` is the user we're logging in as.

Remember – your mission goals are:

* Learn the date they're going to launch their attack
* Learn which type of attack they're planning to launch
* Learn which malware program they're going to use to deploy
* Delete said malware
* Learn the names of the ringleaders

From here, it's down to you to achieve your goals and get out! Here are a couple of hints to help get you started:
- Use `ls` to see a list of the files in the current working directory. The contents of the file `access_logs.json` might help you get started.
- Use the [bash glossary](./bash-glossary.md) to help you navigate through the file system.
- The contents of most files will appear to be gibberish because they have been encoded. Try using `cipher-decode` and entering the filename to decode them!