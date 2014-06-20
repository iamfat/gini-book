# Configuration
All of the configuration files for the Gini framework are stored in the `raw/config` directory in either YAML or PHP format. You'll have to use `gini config update` to update config cache once you modified them.

Sometimes you may need to access configuration values at run-time. You may do so using `_CONF()`:

#### Accessing A Configuration Value
```php
$timezone = _CONF('system.timezone');
```

#### Setting A Configuration Value
```php
_CONF('system.timezone', 'Asia/Shanghai');
```

# Enviroment Configuration
It is often helpful to have different configuration values based on the environment the application is running in. For example, you may wish to use a different cache driver on your local development machine than on the production server. It is easy to accomplish this using environment based configuration.

Simply create a folder within the config directory that matches your environment name with prefix `@`, such as `@development`. Next, create the configuration files you wish to override and specify the options for that environment. For example, to override the database settings for the development environment, you would create a `database.yml` file in `raw/config/@development` with the following content:

```yaml
default:
  dsn: mysql:dbname=test;host=localhost
  username: genee
```
