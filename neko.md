Neko

NEKO_PASSWORD=neko        // Password
NEKO_PASSWORD_ADMIN=admin // Admin Password
NEKO_BIND=0.0.0.0:8080    // Bind
NEKO_KEY=                 // (SSL) Key, needed for clipboard sync
NEKO_CERT=                // (SSL) Cert, needed for clipboard sync

Deploy a server or VPS

Recommended Specs:

Resolution	Cores	Ram	Recommendation
1024×576@30	2	2gb	Not Recommended
1280x720@30	4	3gb	Good Performance
1280x720@30	6	4gb	Recommended
1280x720@30	8	4gb+	Best Performance

curl -sSL https://get.docker.com/ | CHANNEL=stable bash

sudo ufw allow 80/tcp # if you have ufw installed/enabled
sudo ufw allow 59000:59100/udp
wget https://raw.githubusercontent.com/nurdism/neko/master/.examples/simple/docker-compose.yaml
sudo docker-compose up -d

Docker (WIP)
Running:
Chromium container:
sudo docker run -p 80:8080 -p 59000-59100:59000-59100/udp -e NEKO_PASSWORD='secret' -e NEKO_PASSWORD_ADMIN='secret' --cap-add SYS_ADMIN --shm-size=1gb nurdism/neko:chromium
Copy to clipboardErrorCopied
Note: --cap-add SYS_ADMIN & --shm-size=1gb is required for chromium to run properly

Firefox container:
sudo docker run -p 8080:8080 -p 59000-59100:59000-59100/udp -e NEKO_PASSWORD='secret' -e NEKO_PASSWORD_ADMIN='secret' --shm-size=1gb nurdism/neko:firefox 
Copy to clipboardErrorCopied
Note: --shm-size=1gb is required for firefox, tabs will crash otherwise