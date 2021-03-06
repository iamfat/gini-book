# 配置

Gini框架所有的原始配置文件都放在 `raw/config` 目录下面，允许采用YAML或PHP的方式\(PHP方式最好避免\)。修改了配置之后， 你需要在应用目录使用 `gini config update` 命令行命令去更新配置缓冲以使其生效。

#### 访问一个配置值

如果你要在运行时获取配置值，你需要使用`\Gini\Config::get()`：

```php
$timezone = \Gini\Config::get('system.timezone');
```

#### 设置一个配置值

```php
\Gini\Config::set('system.timezone', 'Asia/Shanghai');
```

#### 配置命令行

```bash
# 生成配置缓冲, 确保配置生效
gini cache
# 输出配置
gini config export
gini config export --json
```

# 环境配置

为应用配置多套不同的环境配置是很有帮助的。举个例子，你可能会希望在生产服务器使用和你本地开发环境不一样的缓冲服务，这样这个机制就能帮助你达成这一点而不需要你在部署时反复配置。

你只需要简单的建立一个以 `@` 开头的环境名字命名的文件夹在 `raw/config` 目录下，比如：`@development`。接着，你就可以在这个目录里建立相应同名的配置文件。举个例子，为了在开发环境使用不同的数据库设定，你可以在 `raw/config/@development` 建立一个 `database.yml` 文件：

```yaml
default:
  dsn: mysql:dbname=test;host=localhost
  username: genee
```

当你将环境变量GINI\_ENV设置为你指定的环境名称或通过参数传递环境名称后, 运行 `gini config update` 就会使@development里面的配置生效。

```bash
GINI_ENV=development gini config update
gini cache
```

# 环境变量配置

您可以在代码中使用 `${PLACEHOLDER}`这种方式设置变量，然后在顶层应用通过设置`.env`文件进行设置来达到类似的效果

```yaml
default:
  dsn: mysql:dbname=${DBNAME};host=${DBHOST}
  username: ${DBUSER}
```

然后在 `APP_PATH/.env`录入

```bash
DBNAME=test
DBHOST=localhost
DBUSER=genee
```

执行执行`gini cache`后，相应配置会自动替换。

另外，为了避免默认值不存在影响系统运行，系统支持类似`bash`一样的默认变量设置：

```yaml
default:
  dsn: mysql:dbname=${DBNAME:="abc"};host=${DBHOST:="127.0.0.1"}
```



