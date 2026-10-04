# Docker on EC2 (Amazon Linux) - Quick Notes
 
- **Image vs container:** an image is a read-only template; a container is a running instance of it. One image can run many containers.
- **`dnf install docker`:** installs the Docker engine (daemon `dockerd` plus the `docker` CLI). The CLI just talks to the daemon over a socket.
- **`service docker start` = `systemctl`:** `service` is the legacy SysV-era command. On systemd distros it just forwards to systemctl, so `service docker start` is the same as `systemctl start docker`. The argument order is flipped (`service <name> <action>` vs `systemctl <action> <name>`).
- **Boot gotcha:** like `start`, `service docker start` only runs it for this boot. For boot persistence use `sudo systemctl enable docker` (or `enable --now`), which the tutorial skips.
- **`usermod -a -G docker ec2-user`:** `usermod` modifies a user account. `-G` sets supplementary groups and `-a` appends rather than replacing. Without `-a` you'd be removed from every other group, such as `wheel` (sudo).
- **Why the docker group:** the daemon socket `/var/run/docker.sock` is owned by `root:docker`. Group members can run `docker` without `sudo`. Being in this group is effectively root access, since you can mount the host filesystem into a container.
- **Why logout/login:** group membership is read at login, so existing shells don't see the new group. Verify with `id` or `groups`.
- **`sudo su - ec2-user`:** `su` = switch user. `-` means start a full login shell (loads that user's environment, `$HOME`, PATH). Without it you keep your current environment. `sudo` makes it run as root, then it becomes `ec2-user` with fresh group membership, so you don't need to log out. `newgrp docker` is a lighter alternative.
- **`docker build -t containerofcats .`:** builds an image from the `Dockerfile` in the build context (the `.` = current directory, hence the earlier `cd container`). `-t` gives the image a name/tag.
- **`docker images --filter reference=containerofcats`:** lists local images, filtered by name.
- **`docker run -t -i -p 80:80 containerofcats`:** `-i` keeps stdin open, `-t` allocates a terminal (often written `-it`), and `-p host:container` maps host port 80 to container port 80. It runs in the foreground; add `-d` to run detached (background).
- **Port mapping:** without `-p`, the container's ports aren't reachable from outside. The EC2 security group must also allow inbound port 80.
- **Docker Hub login and tag:** `docker login --username=...`, then `docker tag IMAGEID USER/containerofcats`. Hub names follow `user/repo:tag`, and the tag defaults to `latest`.
- **`docker push USER/containerofcats:latest`:** uploads the image to Docker Hub. Anyone with access can then `docker pull` it.
- **Useful extras:** `docker ps` (running containers), `docker ps -a` (all), `docker stop <id>`, `docker logs <id>`, `docker rm <id>`, `docker rmi <image>`.
 