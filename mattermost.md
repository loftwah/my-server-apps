Ubuntu
Follow the instructions at https://docs.docker.com/installation/ubuntulinux/ or use the summary below:

sudo apt-get update
sudo apt-get install wget
wget -qO- https://get.docker.com/ | sh
sudo usermod -aG docker <username>
sudo service docker start
newgrp docker
Start Docker container:

docker run --name mattermost-preview -d --publish 8065:8065 --add-host dockerhost:127.0.0.1 mattermost/mattermost-preview
When Docker is done fetching the image, open http://localhost:8065/ in your browser.

Sample SMTP Settings
Amazon SES
Set SMTP Username to [YOUR_SMTP_USERNAME]

Set SMTP Password to [YOUR_SMTP_PASSWORD]

Set SMTP Server to email-smtp.us-east-1.amazonaws.com

Set SMTP Port to 465

Set Connection Security to TLS

Postfix
Make sure Postfix is installed on the machine where Mattermost is installed

Set SMTP Username to (empty)

Set SMTP Password to (empty)

Set SMTP Server to localhost

Set SMTP Port to 25

Set Connection Security to (empty)

Gmail
Set SMTP Username to your_email@gmail.com

Set SMTP Password to your_password

Set SMTP Server to smtp.gmail.com

Set SMTP Port to 587

Set Connection Security to STARTTLS

Hotmail
Set SMTP Username to your_email@hotmail.com

Set SMTP Password to your_password

Set SMTP Server to smtp-mail.outlook.com

Set SMTP Port to 587

Set Connection Security to STARTTLS

Office365/Outlook
Set SMTP Username to your_email@hotmail.com

Set SMTP Password to your_password

Set SMTP Server Name to smtp.office365.com

Set SMTP Port to 587

Set Connection Security to STARTTLS

Updating Docker Preview
To delete your existing Docker preview and run a new version use:

docker stop mattermost-preview
docker rm -v mattermost-preview

If you wish to gain access to a shell on the container use:

docker exec -ti mattermost-preview /bin/bash