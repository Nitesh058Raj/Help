# SSH Key Configuration

This guide will walk you through the process of configuring SSH keys for secure authentication on your system.

## Prerequisites

Before you begin, make sure you have the following:

- SSH client installed on your system 
- Access to the remote server you want to connect to

## Step 1: Generate SSH Key Pair

1. Open your terminal or command prompt.
2. Run the following command to generate a new SSH key pair:
    ```
    ssh-keygen -t rsa 
    ```
3. You will be prompted to choose a location to save the key pair. Press Enter to accept the default location.
4. You will also be prompted to enter a passphrase. It is recommended to use a strong passphrase to protect your private key.

## Step 2: Add Public Key to Remote Server

1. Log in to the remote server using your username and password.
2. Create the `~/.ssh` directory if it doesn't exist:
    ```
    mkdir -p ~/.ssh
    ```
3. Append your public key to the `~/.ssh/authorized_keys` file on the remote server:
    ```
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
    ```
4. Set the correct permissions for the `~/.ssh` directory and the `authorized_keys` file:
    ```
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized_keys
    ```
5. Configure ssh with /etc/ssh/sshd_config file, uncomment following lines
    ```
    PubkeyAuthentication yes
    AuthorizedKeysFile      ~/.ssh/authorized_keys
    ```
6. Restart service
    ```
    systemctl restart sshd
    ```

## Step 3: SSH configuration on local machine

1. Download git if not installed and then add ssh, ssh-add, ssh-agent to env variables.
2. create config file in ~/.ssh folder
3. Copy below code
    ```
    Host <Name>
        HostName <HostName or IP addr>
        User <your_username_on_remote_server>
        IdentityFile <C:\path\to\your\private\key>
    ```
4. type ssh-agent on cmd to see below code, then add SSH_AUTH_SOCK, SSHAGET_PID to env variales from that cmd output.
    ```
    SSH_AUTH_SOCK=/tmp/ssh-<random>/agent.<pid>; export SSH_AUTH_SOCK;
    SSH_AGENT_PID=<pid>; export SSH_AGENT_PID;
    echo Agent pid <pid>;
    ```
5. Add keys with ssh-add, then check with ssh-add -l
    ```
    ssh-add C:\path\to\your\private\key
    ssh-add -l
    ```
## Connect with Remote server
1. ssh username@hostname.or.ip.addr
2. Use ssh -v username@hostname.or.ip.addr debugging if not working
3. ssh -i /path/to/private/key username@hostname.or.ip.addr for testing local configuration

## Conclusion

Congratulations! You have successfully configured SSH keys for secure authentication. You can now connect to the remote server without relying on passwords with simple command ssh username@hostname.or.ip.addr.

For more information and advanced configurations, refer to the official documentation of your SSH client and server.