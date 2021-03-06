# SVN info

## 0x01 漏洞描述

在使用SVN管理本地代码过程中，会自动生成一个名为.svn的隐藏文件夹，其中包含重要的源代码信息。一些网站管理员在发布代码时，不愿意使用‘导出’功能，而是直接复制代码文件夹到WEB服务器上，这就使`.svn`隐藏文件夹被暴露于外网环境，黑客可以借助其中包含的用于版本信息追踪的`entries`文件，获取站点信息。

## 0x02 漏洞危害

攻击者可以利用`.svn/entries`文件，获取到应用程序源代码、svn服务器账号密码等信息。同时，SVN产生的`.svn`目录下还包含了以`.svn-base`结尾的源代码文件副本（低版本SVN具体路径为`text-base`目录，高版本SVN为`pristine`目录），如果服务器没有对此类后缀做解析，黑客则可以直接获得文件源代码。

1. 攻击者利用该漏洞可下载网站源代码，获得数据库的连接账号密码等敏感信息；
2. 攻击者可通过获取的源代码进一步分析出新的系统漏洞，从而进一步入侵系统；

## 0x03 修复建议

* 查找服务器上所有.svn隐藏文件夹，删除。
* 开发人员在使用SVN时，严格使用导出功能，禁止直接复制代码。

