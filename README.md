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

1. add the rootkey.pub to the servers .ssh/authorized_keys file (of the user you configured in the "config" file)

2. add new host to "config" file
    ```sshconfig
    Host <hostname>
        Hostname <hostname>
        User <user>
        Port <port> # optional
    ```
3. execute `ssh-keyscan -t ssh-ed25519 [-p <port>] <hostname> >> known_hosts` to add the host to known_hosts
4. add host to ".github/workflows/update-all.yml" file
5. push the changes to this repository
