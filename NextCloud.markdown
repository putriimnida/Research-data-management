# NextCloud
NextCloud is an open-source cloud storage and collaboration platform that allows users to store, share, and synchronize files across devices. It provides seamless access to data and facilitates collaboration with features such as file versioning, shared calendars, and real-time document editing.<br>
You can share one or more files and folders on your computer, and synchronize them with your NextCloud server. Place files in your local shared directories, and those files are immediately synchronized to the server and to other devices using the Nextcloud Desktop Sync Client, Android app, or iOS app.

## Using the Nexcloud web interface
You can upload and download files between Nextcloud and your mobile device or computer, edit files, and share files with other Alliance users.

## Using Nextcloud Desktop Synchronization Client and mobile apps
You can download the Nextcloud Desktop Sync Client or Nextcloud mobile apps to synchronize data from your computer or your mobile device respectively. You can make changes to files locally and they will be updated in Nextcloud automatically.

## Using WebDAV clients
In general, you can use any WebDAV clients to "mount" a Nextcloud folder to your computer using the following WebDAV URL: <https://nextcloud.computecanada.ca/remote.php/webdav/>. Don't forget to enter your username and password!<br>
Once mounted, you can drag and drop files between the WebDAV drive and your local computer.<br>
Mac OSX: Select Go -> Connect to the Server, enter the WebDAV URL for Server Address, and click Connect. You will be asked for your username and password to log in. After authentication, you will see a WebDAV drive on your Mac.<br>
Windows: Use the "Map Network Drive ..." option, select a drive letter, then use WebDAV URL <https://nextcloud.computecanada.ca/remote.php/webdav/> in the Folder field.<br>
You may also consider using Cyberduck or other clients instead. <https://cyberduck.io/> is available for OSX and Windows.<br>
Linux: There are many WebDAV applications available for Linux. Consult <https://docs.nextcloud.com/server/19/Nextcloud_User_Manual.pdf> for recommendations.<br>

## Using UNIX command line tools
You can use any available WebDAV command line clients, like `curl` and `cadaver`, to copy files between your Unix computer and Nextcloud. Command line tools are useful when you want to copy data between a remote server you log in to and Nextcloud.<br>

`curl` is usually installed on Mac OSX and Linux systems and can be used to upload and download files using a URL.<br>
### Upload a file using `curl`
```
[name@server ~]$ curl -k -u <username> -T <filename> https://nextcloud.computecanada.ca/remote.php/webdav/
```

### Download a file using `curl`
```
[name@server ~]$ curl -k -u <username> https://nextcloud.computecanada.ca/remote.php/webdav/<filename> -o <filename>
```

### Upload and download files `rclone`
Unlike `curl`, `rclone` lets you create a configuration once for each remote device and use it repeatedly without having to enter the service details and your password every time. The password will be stored encrypted in *~/.config/rclone/rclone.conf* on the computer or server where the `rclone` command is used.<br>
First, install rclone on your computer if it has a Unix-like environment.<br>
If used from Alliance's clusters, note that it is no necessary to install rclone as it is already available:<br>
```
$ [name@server ~] $ which rclone
$ /cvfs/soft.computecanada.ca/gentoo/2023/x86-64-v3/usr/bin/rclone
```
Next, configure aremote storage device profile with<br>
```
$ rclone config
```
You now have the option to edit an existing remote device, create a new remote device, delete a remote device, and so on. Let's say we want to create a new remote serice profile *nextcloud*:
```
choose "n" for "New remote"
Enter name for new remote --> nextcloud
Type of storage to configure --> 52 / WebDAV
URL of http host to connect to --> https://nextcloud.computecanada.ca/remote.php/dav/files/<your CCDB username>
Name of the WebDAV site/service/software you are using --> 2 / Nexcloud
User name --> <your CCDB username>
choose "y" for "Option pass"
Password --> <your CCDB password">
Leave "Option bearer_token" empty
choose "no" for "Edit advanced config"
choose "yes" for "Keep this 'nextcloud' remote"
choose "q" to quit config
```
You should now be able to see your new remote service profile in the list of configured ones with<br>
```
$ rclone listremotes
```
You can probe available disk space with
```
$ rclone about nextcloud
```
To upload a file, run
```
$ rclone copy /path/to/local/file nextcloud:remote/path
```
To download a file, run
```
$ rclone copy nextcloud:remote/path/file .
```

## Sharing files using Nextcloud
When you select a file or directory to share, type the user's first name, last name, or username and the list of matched users registered in CCDB (Compute Canada Database) will be displayed in "Firstname Listname (username)" format. Please review the name carefully as some are very similar; in doubt, enter the username which is unique. You can also share files with a group using their CCDB group name (default, RPP, RRG, or other shared groups). To share a file with people who don't have an Alliance account, use the *Share link* option and provide their email address. Nextcloud will send an email notification with a link to access the file.<br>
RRG: Resources for Research Groups<br>
RRP: Research Platforms and Portals<br>


Source: https://docs.alliancecan.ca/wiki/Nextcloud
