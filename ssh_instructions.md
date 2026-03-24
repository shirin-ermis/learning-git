    - Instructions (via Software Carpentry, the [full course on version control](https://swcarpentry.github.io/git-novice/) is very helpful if you have the time)
        
        To create an SSH key pair Vlad uses this command, where the `-t` option specifies which type of algorithm to use and `-C` attaches a comment to the key (here, Vlad’s email):
        
        `$ ssh-keygen **-t** ed25519 **-C** "vlad@tran.sylvan.ia"`
        
        If you are using a legacy system that doesn’t support the Ed25519 algorithm, use: `$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
        
        `Generating public/private ed25519 key pair.
        Enter file in which to save the key (/c/Users/Vlad Dracula/.ssh/id_ed25519):`
        
        We want to use the default file, so just press Enter.
        
        `Created directory '/c/Users/Vlad Dracula/.ssh'.
        Enter passphrase (empty for no passphrase):`
        
        Now, it is prompting Dracula for a passphrase. Since he is using his lab’s laptop that other people sometimes have access to, he wants to create a passphrase. Be sure to use something memorable or save your passphrase somewhere, as there is no “reset my password” option.
        
        `Enter same passphrase again:`
        
        After entering the same passphrase a second time, we receive the confirmation
        
        `Your identification has been saved in /c/Users/Vlad Dracula/.ssh/id_ed25519
        Your public key has been saved in /c/Users/Vlad Dracula/.ssh/id_ed25519.pub
        The key fingerprint is:
        SHA256:SMSPIStNyA00KPxuYu94KpZgRAYjgt9g4BA4kFy3g1o vlad@tran.sylvan.ia
        The key's randomart image is:
        +--[ED25519 256]--+
        |^B== o.          |
        |%*=.*.+          |
        |+=.E =.+         |
        | .=.+.o..        |
        |....  . S        |
        |.+ o             |
        |+ =              |
        |.o.o             |
        |oo+.             |
        +----[SHA256]-----+`
        
        The “identification” is actually the private key. You should never share it. The public key is appropriately named. The “key fingerprint” is a shorter version of a public key.
        
        Now that we have generated the SSH keys, we will find the SSH files when we check.
        
        `ls **-al** ~/.ssh`
        
        `drwxr-xr-x 1 Vlad Dracula 197121   0 Jul 16 14:48 ./
        drwxr-xr-x 1 Vlad Dracula 197121   0 Jul 16 14:48 ../
        -rw-r--r-- 1 Vlad Dracula 197121 419 Jul 16 14:48 id_ed25519
        -rw-r--r-- 1 Vlad Dracula 197121 106 Jul 16 14:48 id_ed25519.pub`
        
        **Copy the public key to GitHub**
        
        Now we have a SSH key pair and we can run this command to check if GitHub can read our authentication.
        
        `ssh **-T** git@github.com`
        
        `The authenticity of host 'github.com (192.30.255.112)' can't be established.
        RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
        This key is not known by any other names
        Are you sure you want to continue connecting (yes/no/[fingerprint])? y
        Please type 'yes', 'no' or the fingerprint: yes
        Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
        git@github.com: Permission denied (publickey).`
        
        Right, we forgot that we need to give GitHub our public key!
        
        First, we need to copy the public key. Be sure to include the `.pub` at the end, otherwise you’re looking at the private key.
        
        `cat ~/.ssh/id_ed25519.pub`
        
        `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDmRA3d51X0uu9wXek559gfn6UFNF69yZjChyBIU2qKI vlad@tran.sylvan.ia`
        
        Now, going to GitHub.com, click on your profile icon in the top right corner to get the drop-down menu. Click “Settings,” then on the settings page, click “SSH and GPG keys,” on the left side “Account settings” menu. Click the “New SSH key” button on the right side. Now, you can add the title (Dracula uses the title “Vlad’s Lab Laptop” so he can remember where the original key pair files are located), paste your SSH key into the field, and click the “Add SSH key” to complete the setup.
        
        Now that we’ve set that up, let’s check our authentication again from the command line.
        
        `$ ssh **-T** git@github.com`
        
        `Hi Vlad! You've successfully authenticated, but GitHub does not provide shell access.`
        
        Good! This output confirms that the SSH key works as intended. We are now ready to push our work to the remote repository.
        
        **If this does not work**, try adding the key to the ssh config file, type `open ~/.ssh/config`, then add the following
        
        ```bash
        Host github.com
          AddKeysToAgent yes
        	IgnoreUnknown UseKeychain # This line solved a problem with usekeychain option
          UseKeychain yes
          IdentityFile ~/.ssh/id_ed25519
        ```
        
        Reference for this last bit is 
        
        [Generating a new SSH key and adding it to the ssh-agent - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
        
