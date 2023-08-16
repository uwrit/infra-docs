# Set up using SSH

In order to access services within the Research IT network, you must setup an SSH tunnel to pass your traffic through to the protected server.

> **Windows SSH Command Prompt Install**

> Windows users should use the "Git Bash" shell to install the needed SSH tools to complete the steps below and get a Linux style command prompt. Git's toolset isn't installed by default on Windows and so you will need to download it.

> Install Git Tools: <a href="https://git-scm.com/downloads" target="_blank">https://git-scm.com/downloads</a>

> Ensure that you install "Git Bash" and open it to get a command prompt.

## Getting Started

### SSH Keypair Creation (on the command line)

Create a `.ssh` folder in your user's home folder, and then store your key.

1. Open up the **Command Prompt** on Mac OS/Linux or Windows.

2. Create an SSH configuration directory:

		mkdir ~/.ssh

3. Create a new SSH keypair:

		ssh-keygen -t ed25519 -b 521 -f ~/.ssh/<my_private_sshkey>
   or:

		ssh-keygen -t ecdsa -b 521 -f ~/.ssh/<my_private_sshkey>

> Note: Ensure that you enter a strong password to protect the keypair and protect that password.

4. Once the key is created, send the contents of the public key text file (my_private_sshkey.pub in the example above) to <a href="mailto:rithelp@uw.edu">rithelp@uw.edu</a> with your name and UW NetID.

	**Tip**: Output contents of files to the screen using the `cat` command:
		
		cat ~/.ssh/my_private_sshkey.pub
> Note: The Research IT group will put that public key file on each server you need access to. You won't be able to login to your server until we've applied this public key to your profile.

### SSH Config File Customization

Create a file called `config` in the `.ssh` folder which will save your connections.

1. In the command prompt, run the command
	
		touch ~/.ssh/config

2. Edit the `~/.ssh/config` file using an editor and add the following text:
```bash
# Read more about SSH config files: https://linux.die.net/man/5/ssh_config
IdentityFile ~/.ssh/<my_private_sshkey>
User <uwnetid>

# remote bastion required in order to access other machines
host remote 
    HostName remote.rit.uw.edu

# ssh proxy example 
host <example-host>
    HostName <example-host>.rit.uw.edu
    ProxyJump remote

# port forward example - mostly used for database machines
host <db-example>
    HostName <db-host>.rit.uw.edu
    ProxyJump remote
    LocalForward <db-port> localhost:<db-port>
```

> Note: The above "port forward example" forwards local port to the remote desktop port on the internal server db-example.rit.uw.edu.

## Examples

### Connecting Directly

To log in to any machine (including db machines), run:

	ssh <example-host>

> Note: You will be prompted twice to enter your SSH key password.

After a successful login, you should be able to use the machine through the command line.

### Port Forwarding

Once logged in to the port forwarding tunnel, your command line window will show that you are logged into `remote`.

	username@remote $

> Note: The forwarded port will always be connected to via 'localhost' or 127.0.0.1.

You won't be using this command line window any further, but you do need to leave this window open. When you are done working you will return to this window to exit out of the tunnel connection. If you close the command line or "Git Bash" window, it will close your ssh tunnel session.
