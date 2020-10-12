### on arch linux base-devel pakage is needed
`$sudo pacman -S bc base-devel`

### creat a folder on home
`$mkdir newkernel`
`$cd newkernel`

### clone torvalds git
`$git clone https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/`

* and download config-wsl compile file
`$wget https://raw.githubusercontent.com/microsoft/WSL2-Linux-Kernel/linux-msft-wsl-4.19.y/Microsoft/config-wsl`

* Open it and edit CONFIG_LOCALVERSION and save
`$code config-wsl`

* Move config-wsl to:
`$mv config-wsl linux/arch/x86/configs/wsl_defconfig`

`$cd linux`

`$make wsl_defconfig`

`$make -j6`

* Now copy vmlinux to user folder
`$cp vmlinux /mnt/c/Users/Morty`

* create .wslconfig file and add:
```
[wsl2]
kernel=C:\\Users\\Morty\\vmlinux
```

### Check Kernel Version by neofetch or uname -a
