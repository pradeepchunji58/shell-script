# shell-script

1. Create Shell Script

Open terminal and create an empty shell script using the following command.

$ sudo vi data_backup.sh


2. Add shell script to backup files

Here is the tar command to backup files in a directory /home/data to backup.tar.gz. You can replace the directory path and backup file name below as per your requirement.

$ sudo tar -cvpzf /home/backup.tar.gz /home/data

In the above command,

c – compression
v – verbose
p – retain file permissions
z – create gzip file
f – regular file

Now add the following to your shell script.

#!/bin/sh
timestamp="$(date +'%b-%d-%y')"
sudo tar -cvpzf /home/backup-${timestamp}.tar.gz /home/data

Save and close the file. In the above code, the first line sets the execution environment, the second line saves timestamp value and the third line does the backup by creating .tar.gz file. We use the timestamp variable to create a new filename every time the script is run so that the backups remain separate and there is no overwriting.


3. Make Script Executable

Run the following command to make your script executable.

$ sudo chmod +x data_backup.sh


4. Verify the script

Run the script with following command.

$ sudo /home/data_backup.sh


5. Automate Backup

It is advisable to create a cron job to run the above script regularly in an automatic manner. For this, open crontab with the following command.

$ sudo crontab -e

Add the following line to run the above shell script regularly every day at 10 a.m

0 10 * * * sudo /home/data_backup.sh >/dev/null 2>&1

Save & close the file. In the above command, “0 10 * * *” ensures that the our shell script runs every day at 10 am. Also, we mute the execution result by sending the output to /dev/null.

If you wish to make your script dynamic to be able to accept folder name dynamically then update the last line of your shell script as following

sudo tar -cvpzf /home/backup-$timestamp.tar.gz $1

In this case, you can call the shell script to backup any folder by passing it as command line argument.
$ sudo /home/data_backup.sh /home/data

Update the cronjob command as following to pass the folder name dynamically as you wish.

0 10 * * * sudo /home/data_backup.sh /home/data >/dev/null 2>&1

In this article, we have learnt how to automatically backup files & directory using shell script & cronjob.
