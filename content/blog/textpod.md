---
title: Textpod
description: Hosting a textpod server for myself on oracle cloud
date: 2024-12-01
tags: 
---
### Oracle
Made a free account for oracle cloud. Provisioned a linux instance.

### Docker
Update package manager
```
sudo yum update
```

Add `yum-utils` and docker repo
```
sudo dnf install -y dnf-utils zip unzip
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
```

Install Docker
```
dnf remove -y runc
dnf install -y docker-ce --nobest
```

Gave up getting docker on oracle cloud free machine.

Trying to just install textpod with cargo instead.

Install Cargo:
```
curl https://sh.rustup.rs -sSf | sh
```

Install textpod:
```
cargo install textpod
```

---
The free machine is just too slow. Got a E3.Flex instead.

Made sure routing was working for apache: https://docs.oracle.com/en/learn/lab_compute_instance/index.html#troubleshooting

Installing docker this time. :pray:
https://oracle-base.com/articles/linux/docker-install-docker-on-oracle-linux-ol8

Ok working, used this nginx reverse proxy thing to route a subdomain: https://github.com/nginx-proxy/nginx-proxy?tab=readme-ov-file
Not sure if I did that right but it works for http://notes.austinwillis.com to go to the textpod container.


Ooooh, nice: http://worknotes.austinwillis.com

Started another container of textpod:
```
sudo docker run --detach --rm --name textpod2 -d -v $(pwd)/notes:/app -p 8081:3000 --env VIRTUAL_HOST=worknotes.austinwillis.com freetonik/textpod
```
This routes the other subdomain to a differnt notes server with a new file.
