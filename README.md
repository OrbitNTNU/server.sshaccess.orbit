# Server SSH Access

This repository automatically distributes "authorized_keys" files to servers.

On a push to this repository, all authorized_keys files are updated on all servers.

## Usage

1. find or create the key you want to add (e.g. `~/.ssh/id_rsa.pub`)
2. add the key to the `authorized_keys.<servername>` file in this repository (for the server you want to get access to)
3. push the changes to this repository

## Add host

This script connects to the server via SSH with the rootkey to update the authorized_keys file.

For this script to work it needs SSH access to the server. For this the server needs to have the contents of the rootkey.pub in the servers authorized_keys file.

### Prepare server

1. You need to have SSH access to the server. Note down the Hostname and the User you want to use.
2. add the rootkey_*.pub from this repository to the servers ~/.ssh/authorized_keys file (in the users home directory)

### Configure repository

3. add new host to "config" file
    ```sshconfig
    Host <hostname>
        Hostname <hostname>
        User <user>
        Port <port> # optional
    ```
4. add host to ".github/workflows/update-all.yml" file
5. push the changes to this repository

### Server SSH configuration

6. Now check with your own key if you have access to the server
    ```bash
    ssh <user>@<hostname
    ```
7. ONLY CONTINUE IF YOU HAVE ACCESS WITHOUT NEEDING A PASSWORD
8. Now you need to disable password login and root login via SSH
    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
    find and change the following lines
    ```sshd_config
    PasswordAuthentication no
    PermitRootLogin no
    ```

9. restart the SSH service
    ```bash
    sudo systemctl restart sshd
    ```
