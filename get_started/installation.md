# Installation
### Download Gini
```bash
mkdir $HOME/gini-modules
cd $HOME/gini-modules
git clone https://github.com/iamfat/gini.git
```

### Server Requirements
Gini framework has following system requirements:

* PHP >= 5.4
* PHP YAML Extension installed

### Use Gini for Current User
1. Put following lines to `~/.profile`
```bash
export PATH=$HOME/gini-modules/gini/bin:$PATH
```

### Use Gini for All Users
1. You'd better make a `phar` build before
```bash
$ cd `gini root`
$ composer update
$ gini build
$ tree -L 1 build
build
└── gini
```

2. Deploy the build to `/usr/local/share/gini` and setup a place to put gini modules
```bash
sudo mkdir -p /usr/local/share/gini-modules
sudo cp -r build/gini /usr/local/share/gini-modules
```

3. Put following lines to /etc/profile
```bash
export PATH=/usr/local/share/gini/bin:$PATH
```
