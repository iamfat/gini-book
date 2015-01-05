# 安装
### 下载 Gini
```bash
mkdir $HOME/gini-modules
cd $HOME/gini-modules
git clone https://github.com/iamfat/gini.git
```
如果你用Docker的话, 你可以很容易的获得一个完全准备好的Gini开发环境
```bash
docker pull genee/gini-dev
docker run --name gini-dev -d -p 9000:9000 genee/gini-dev
```

### 对系统环境的要求
Gini 框架需要你的系统至少有:

* PHP >= 5.4
* PHP YAML 扩展


### 在当前的用户中使用 Gini
1. Put following lines to `~/.profile`
```bash
export PATH=$HOME/gini-modules/gini/bin:$PATH
```

### 在全局环境使用 Gini
1. Deploy the build to `/usr/local/share/gini` and setup a place to put gini modules
```bash
mkdir -p /usr/local/share/gini-modules
git clone https://github.com/iamfat/gini /usr/local/share/gini-modules/gini
```

2. Put following lines to `/etc/profile.d/gini.sh
```bash
export PATH=/usr/local/share/gini/bin:$PATH
```
