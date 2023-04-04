
Note: The scripted web delivery must hosta  smb payload and encode de download as:

http://proxymachine:8080/x

Why? Because proxymachine has a reverse port forward: (incoming from 8080 -> localteamserver:80)  since the target executing the download cannot conect directly.

