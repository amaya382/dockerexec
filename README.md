# This project has been deprecated. Use anyrc instead.

[amaya382/anyrc](https://github.com/amaya382/anyrc)


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
git clone git@github.com:amaya382/dockerexec.git
ln -s `pwd`/dockerexec/.dockershrc ~/dockershrc
ln -s `pwd`/dockerexec/.dockershrc.d ~/dockershrc.d
sudo cp dockerexec/dockerexec /usr/local/bin

docker run --name foo -d --rm nginx:alpine
dockerexec foo zsh
# zsh not found in foo. install? [y/n] y
ll # on zsh w/ colored prompt
# total 52
# -rwxr-xr-x    1 root     root             0 Dec 21 22:40 .dockerenv*
# drwxr-xr-x    1 root     root          4096 Dec 21 22:41 bin/
# drwxr-xr-x    5 root     root           340 Dec 21 22:40 dev/
# drwxr-xr-x    1 root     root          4096 Dec 21 22:41 etc/
# drwxr-xr-x    2 root     root          4096 Dec  1 16:32 home/
# ...
apk add --no-cache vim tmux
vim /etc/nginx/nginx.conf # w/ line number
#  1
#  2 user  nginx;
#  3 worker_processes  1;
#  4
#  5 error_log  /var/log/nginx/error.log warn;
#  6 pid        /var/run/nginx.pid;
#  ...
tmux # on zsh w/ datetime prompt
```

### Options
* You can use arbitrary `.dockershrc` and `.dockershrc.d` by passing via `${SHRC}` and `${SHRCD}`
  * `SHRC=/path/to/.dockershrc SHRCD=/path/to/.dockershrc.d dockerexec ...`
