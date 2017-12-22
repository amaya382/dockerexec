# dockerexec
A tiny wrapper for `docker exec -it`. Bring your `.bashrc`, `.zshrc`, `.vimrc`, etc into docker container, like [sshrc](https://github.com/Russell91/sshrc).

## How to use
1. Create `.dockershrc.d` in your `${HOME}` and put your dotfiles into it
2. Put `.dockershrc` into your `${HOME}` and edit it
3. Put `dockerexec` into your `${PATH}` dir (e.g. `/usr/local/bin`)
4. `dockerexec [opts] $container_name $shell_name`

## Example
```sh
cd
mkdir .dockershrc.d
echo 'alias ll="ls -Al"' > .dockershrc.d/.zshrc
echo 'set number' > .dockershrc.d/.vimrc
wget https://github.com/amaya382/dockerexec/raw/master/.dockershrc
wget https://github.com/amaya382/dockerexec/raw/master/dockerexec
chmod +x dockerexec
sudo mv dockerexec /usr/local/bin

docker run --name foo -d --rm nginx:alpine
dockerexec foo zsh
# zsh not found in foo. install? [y/n] y
ll
# total 52
# -rwxr-xr-x    1 root     root             0 Dec 21 22:40 .dockerenv*
# drwxr-xr-x    1 root     root          4096 Dec 21 22:41 bin/
# drwxr-xr-x    5 root     root           340 Dec 21 22:40 dev/
# drwxr-xr-x    1 root     root          4096 Dec 21 22:41 etc/
# drwxr-xr-x    2 root     root          4096 Dec  1 16:32 home/
# ...
apk add --no-cache vim
vim /etc/nginx/nginx.conf
#  1
#  2 user  nginx;
#  3 worker_processes  1;
#  4
#  5 error_log  /var/log/nginx/error.log warn;
#  6 pid        /var/run/nginx.pid;
#  ...
```

### Options
* You can use arbitrary `.dockershrc` and `.dockershrc.d` by passing via `${SHRC}` and `${SHRCD}`
  * `SHRC=/path/to/.dockershrc SHRCD=/path/to/.dockershrc.d dockerexec ...`
