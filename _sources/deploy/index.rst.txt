.. _deploy:


.. toctree::
   :hidden:

   example


环境要求
------------


目前支持部署环境仅 **Linux** 和 **mac** 且系统中必须安装Google chrome 64版本，或者需要将对应的chromedriver放入到项目执行路径下。


部署前需要准备的是

1. postgresql 数据库，创建monitoring数据库，并支持hstore
#. redis 数据库，将用于队列存储。如、celery的消息队列、在后续可以用于爬虫的url队列、搭建分布式爬虫。
#. python3 和 pip3


安装python第三方库
------------------


一般的我们在开发环境会为将功能细分、将python环境分割开，避免第三方库的版本冲突，或是因为系统升级导致不必要的问题。那么在生产环境，我们默认系统不会升级(最多打安全补丁)，当然可以自行创建python环境，用于隔离系统python环境，这里将不进行过多叙述。

一般的我们的项目目录下会有文件requirements.txt，请在终端执行 pip3 install -r requirements.txt 用于安装第三方库。
在安装的过程中可能会出现一些驱动的问题，不同的环境可能不一样，请到该库相应的官网查看相应的处理办法。

配置文件
---------

本项目是可配置的，配置文件基本都是以toml格式的，相应语法请自行查询相应资料，这里将不进行大篇幅介绍。



monitoring的项目配置
>>>>>>>>>>>>>>>>>>>>>>>>

配置文件路径 `conf/base.toml`

1. 其中 `secret_key` 是session的加密密钥、而session存储在客服端、所以为两安全起见、`secret_key` 值在生产环境中必须更改
#. celery, 这里将配置celery队列存储的环境，及结果存储位置，当然还可以配置其他的，这里将不介绍。
#. 数据库配置，主要修改db.params里面的数据库信息、如user,以及其他的。
#. 远程浏览器配置，这里可以是selenium的服务地址，也可以是chromedriver的地址，建议使用chromedriver的地址，它将传入适当参数，即可支持远程，而selenium目前对chrome不支持远程。


其他更多配置，请查看配置文件，那里有相应的介绍。

百度网盘爬虫配置
>>>>>>>>>>>>>>>>>>>>>>

配置文件路径 `conf/base.toml`

详细配置请看配置文件。

值得注意的是目前支持的邮箱只有qq邮箱和163邮箱、不同的邮箱对邮件内容的编码不一样，所以在解析验证码的时候会出错。
这里也要配置数据库，请按照需要配置。

日志这里也支持错误日志邮件，默认是注释，如有需求，自行配置。

scrapyd的配置
>>>>>>>>>>>>>>>>>>

配置方法请查看官网https://doc.scrapy.org/en/latest/topics/scrapyd.html

chromedriver 配置
>>>>>>>>>>>>>>>>>>>>>

国内下载地址http://npm.taobao.org/mirrors/chromedriver/
配置方法请查看对应官网和版本。

supervisord的配置
>>>>>>>>>>>>>>>>>>>>>

详细配置请查看官网http://supervisord.org/introduction.html

这里将管理我们已上的项目进程，用于方便启动，同时可以根据自己需求，将nginx、redis、postgresql、的启动也放入此处。


运行
-----------
supervisord







