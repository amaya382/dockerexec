# dockerexec
A tiny wrapper for `docker exec -it`. Bring your `.bashrc`, `.zshrc`, `.vimrc`, etc into docker container.

## How to use
1. Create `.dockershrc.d` in your `${HOME}` and put your dotfiles into it
2. Put `.dockershrc` into your `${HOME}` and edit it
3. Put `dockerexec` into your `${PATH}` dir (e.g. `/usr/local/bin`)
4. `dockerexec [opts] $container_name $shell_name`

### Options
* You can use arbitrary `.dockershrc` and `.dockershrc.d` by passing via `${SHRC}` and `${SHRCD}`
  * `SHRC=/path/to/.dockershrc SHRCD=/path/to/.dockershrc.d dockerexec ...`
