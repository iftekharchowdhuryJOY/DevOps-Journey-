# Archiving and Transferring files
Archiving and compressing files are useful when creating backups and transferring data across a network.
tar command: users can gather large sets of files into a single file (archive).

options:
-c: create a new archive 
-x: extract from an archive 
-t: list the table of contents of an archive 
-v: verbose
-f: file name.
-p: preserve the permissions of files and directories when extracting from an archive 
-z: use gzip compression
-j: --bzip compression
-J: xz compression 
The following command creates an archive named archive.tar with the contents of file1, file2, and file3 in the user's home directory.
`tar -cf archive.tar file1 file2 file3`
- LISTING CONTENTS OF AN ARCHIVE: tar -tf /root/etc.tar
- EXTRACTING FILES FROM AN ARCHIVE: tar -xf x.tar
### CREATING A COMPRESSED ARCHIVE: 
To create a gzip compressed archive named /root/etcbackup.tar.gz, with the contents from the /etc directory on host: tar -czf /root/etcbackup.tar.gz /etc
To create a bzip2 compressed archive named /root/logbackup.tar.bz2, with the contents from the /var/log directory on host: tar -cjf /root/logbackup.tar.bz2 /var/log

## TRANSFERRING FILES USING SECURE COPY
The Secure Copy command, scp, which is part of the OpenSSH suite, copies files from a remote system to the local system or from the local system to a remote system.
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
To copy a file from a local to a remote system, run the following command:scp file.txt remote_username@10.10.0.2:/remote/directory
To copy a directory and all its files, invoke the scp command with the -r flag, which recursively copies the entire directory and its contents:scp -r /local/directory remote_username@10.10.0.2:/remote/directory
copy a file from a remote system to the local file system. In this example, the file /etc/hostname on remotehost is copyed to the local directory /home/user.
The scp command authenticates to remotehost as the user remoteuser: scp remoteuser@remotehost:/etc/hostname /home/user

## TRANSFERRING FILES USING THE SECURE FILE TRANSFER PROGRAM
To interactively upload or download files from a SSH server, use the Secure File Transfer Program, sftp.

## SYNCHRONIZING FILES BETWEEN SYSTEMS SECURELY
The rsync command is another way to securely copy files from one system to another. 
