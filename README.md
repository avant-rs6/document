基于ThinkPHP5.0的文档生成插件
==========

* [安装要求](#requirements)
* [安装](#installation)
* [使用方式](#usage)
* [可以使用的参数](#methods)

### <a id="requirements"></a>安装要求

PHP >= 5.3.2

thinkphp = 5.0.*

### <a id="installation"></a>安装

使用composer安装

```bash
$ composer require zhangzhuow/document
```
### <a id="usage"></a>使用方式

```php
<?php

namespace Document\Command;

/**
 * @ApiTitle  (name)  此参数为必须
 */
class User
{
    /**
     * @ApiTitle  (name)  此参数为必须
     * @ApiDescription(section="User", description="Get information about user")
     * @ApiMethod(type="get")
     * @ApiRoute(name="/user/get/{id}")
     * @ApiParams(name="id", type="integer", nullable=false, description="User id")
     * @ApiParams(name="data", type="object", sample="{'user_id':'int','user_name':'string','profile':{'email':'string','age':'integer'}}")
     * @ApiReturnHeaders(sample="HTTP 200 OK")
     * @ApiReturn(type="object", sample="{
     *  'transaction_id':'int',
     *  'transaction_status':'string'
     * }")
     */
    public function get()
    {

    }

    /**
     * @ApiTitle  (name)  此参数为必须
     * @ApiDescription(section="User", description="Create's a new user")
     * @ApiMethod(type="post")
     * @ApiRoute(name="/user/create")
     * @ApiParams(name="username", type="string", nullable=false, description="Username")
     * @ApiParams(name="email", type="string", nullable=false, description="Email")
     * @ApiParams(name="password", type="string", nullable=false, description="Password")
     * @ApiParams(name="age", type="integer", nullable=true, description="Age")
     */
    public function create()
    {

    }
}
```

配置command.php文件，目录在application/command.php

```php
<?php
return [
    'app\home\command\Test',
];

```

将扩展包config文件夹内的site.php拷贝至application/extra文件夹

执行ThinkPHP命令行会新增一个api命令

```php
$ php think -l

Think Console version 0.1

Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -V, --version         Display this console version
  -q, --quiet           Do not output any message
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Available commands:
  api                 从控制器构建API文档
  build               Build Application Dirs
  clear               Clear runtime file
  help                Displays help for a command
  list                Lists commands
 make
  make:controller     Create a new resource controller class
  make:model          Create a new model class
```

执行api命令生成html文档

```php
$ php think api
```

html文档位置为public目录

### <a id="methods"></a>可以使用的参数

* @ApiTitle (name)
* @ApiDescription(section="...", description="...")
* @ApiMethod(type="(get|post|put|delete|patch")
* @ApiRoute(name="...")
* @ApiParams(name="...", type="...", nullable=..., required="...", value="...", description="...", [sample=".."])
* @ApiHeaders(name="...", type="...", nullable=..., required="...", value="...", description="...")
* @ApiReturnHeaders(sample="...")
* @ApiReturn(type="...", sample="...")
* @ApiBody(sample="...")

只会生成带有@ApiTitle参数的方法和类


