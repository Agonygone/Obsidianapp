---
url: https://www.temdu.com/2018/03/65.html
title: 通过 Office 发送文章到 Typecho 博客 - 天度视界
date: 2023-06-28 14:22:01
tag: 
summary: Office 在 2007 及以后的版本中加入了发送文章到博客的功能，功能如图所示今天又在某主题售后群吹水时得知这一功能，大致搜索了一下 Office 的这个功能，发现是通过 XMLRPC 接口实现的，正好...
---
*   博主： [Hmm](https://www.temdu.com/author/1/)
*   发布时间：2018 年 03 月 20 日
*   8897 次浏览
*   [5 条评论](#comments)
*   551 字数
*   分类： [默认分类](https://www.temdu.com/category/default/)

sr-annote { all: unset; }

1.  [首页](https://www.temdu.com/)
2.  正文  

分享到：[](https://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey?url=https://www.temdu.com/2018/03/65.html&title=%E9%80%9A%E8%BF%87Office%E5%8F%91%E9%80%81%E6%96%87%E7%AB%A0%E5%88%B0Typecho%E5%8D%9A%E5%AE%A2&site=https://www.temdu.com/)[](https://service.weibo.com/share/share.php?url=https://www.temdu.com/2018/03/65.html&title=%E9%80%9A%E8%BF%87Office%E5%8F%91%E9%80%81%E6%96%87%E7%AB%A0%E5%88%B0Typecho%E5%8D%9A%E5%AE%A2)

Office 在 2007 及以后的版本中加入了发送文章到博客的功能，功能如图所示

今天又在某主题售后群吹水时得知这一功能，大致搜索了一下 Office 的这个功能，发现是通过 XMLRPC 接口实现的，正好 Typecho 也带有 XMLRPC 接口，稍微测试了一下发现 Ofiice 的发送文章到博客功能也支持 Typecho，具体设置方法如下：

1.  首先在 Typecho 后台打开 XMLRPC 接口，具体设置位于后台 > 设置 > 基本 > XMLRPC 接口 > 打开  
    
2.  再到 Office 添加博客账号，设置如下这里选择其他然后点击下一步，Typecho 的 XMLRPC 接口的地址是 http:// 博客域名 / action/xmlrpc 具体如图注意需要账号和密码，输入完成后确定就将自己的博客信息保存到了 Office。  
    
3.  在 Office 编辑文章。  
    
4.  点击 Office 左上角的发布按钮将文章发布到博客。  
    

总结：能用 Office 编辑文章确实比较方便，并且 Typecho 的 XMLPRC 接口也支持 Markdown 语法解析就更完美了，当然本教程比较简略，详细的可以百度参考 Office 发布文章到其他博客等，具体操作大致都一样，唯一不同的就是 XMLPRC 接口，当然我也给出了 Typecho 的 XMLPRC 接口地址，相信安装教程设置是不会有问题的。