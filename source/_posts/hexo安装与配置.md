---
title: Hexo 安装与配置
tags: 
 - hexo 安装
categories: 
 - Hexo
 - Hello world
---
hexo安装与配置
=========
#### hexo部署到github

1、[安装git](https://links.jianshu.com/go?to=https%3A%2F%2Fgit-scm.com%2Fdownload%2Fwin)

2、[安装nodejs](https://links.jianshu.com/go?to=https%3A%2F%2Fnodejs.org%2Fen%2F)

3、用 npm 安装话经常出现卡住而导致无法正常安装，解决办法就是修改 npm 的安装源，这里选择淘宝 NPM 镜像，这是一个完整 npmjs.org 镜像，你可以用此代替官方版本，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。

    npm config set registry https://registry.npm.taobao.org


4、安装hexo

    npm install -g hexo-cli


![](https://upload-images.jianshu.io/upload_images/4117703-d6ac5a647408635f.png?imageMogr2/auto-orient/strip|imageView2/2/w/962/format/webp)

安装hexo

5、查看版本信息

    hexo -v


![](https://upload-images.jianshu.io/upload_images/4117703-1f078303534ecbc2.png?imageMogr2/auto-orient/strip|imageView2/2/w/291/format/webp)

查看版本信息

6、初始化hexo程序

    hexo init myblog


（更新npm/并更换为国内的npm镜像命令：npm install npm -g/  
npm install -g cnpm --registry=[https://registry.npm.taobao.org](https://links.jianshu.com/go?to=https%3A%2F%2Fregistry.npm.taobao.org)）

7、进入myblog文件夹

    cd myblog


（8、`npm install`）

9、查看文件夹目录

*   node\_modules: 依赖包
*   scaffolds：生成文章的一些模板
*   source：用来存放你的文章
*   themes：主题
*   \*\* \_config.yml: 博客的配置文件\*\*

![](https://upload-images.jianshu.io/upload_images/4117703-802043b47789dde5.png?imageMogr2/auto-orient/strip|imageView2/2/w/178/format/webp)

文件夹目录

10、打开hexo

    hexo g
    hexo server


11、创建以用于提交

    git config --global user.name "yourname"
    git config --global user.email "youremail"


12、连接公钥

    ssh-keygen -t rsa -C "email"


13、查看是否成功

    ssh -T git@github.com


（You've successfully authenticated, but GitHub does not provide shell access.）

14、将hexo和GitHub关联起来，修改配置文件\_config.yml

    deploy:
      type: （中间有个空格，以下相同）git
      repo: https://github.com/YourgithubName/YourgithubName.github.io.git
      branch: master


15、安装deploy-git部署命令

    npm install hexo-deployer-git --save


16、清除之前生成的东西

    hexo clean


17、生成静态文章

    hexo generate/hexo g


18、部署文章

    hexo deploy/hexo d


19、github中要新建一个仓库用户名+github.io，访问用户名.github.io即可

#### 设置hexo主题

1、[选择hexo主题](https://links.jianshu.com/go?to=https%3A%2F%2Fhexo.io%2Fthemes%2F)，到github上下载主题放到themes文件夹下  
2、修改\_config.yml里的theme为该文件夹名称

#### 新增菜单栏选项

1、添加新页面：hexo new page "xx"  
2、在主题配置文件的menu中加上该页面  
3、在zh-CN.yml文件中加上中文意思

#### 新增草稿

1、添加草稿：hexo new draft "xx"  
2、预览草稿：hexo server --draft  
3、发布草稿：hexo publish draft "xx"

#### 图片处理

1、配置文件中的post\_asset\_folder改成true  
2、npm install hexo-asset-image --save  
3、放到该文件夹下，按照md格式输入(文件名称/图片名.jpg)

##### 搜索

1、npm install hexo-generator-searchdb --save  
2、站点配置文件的扩展下添加

    search:
      path: search.xml
      field: post
      format: html
      limit: 10000


3、主题配置文件下，local\_search改成true即可

    local_search:
      enable: true


##### 字数

1、npm install hexo-symbols-count-time --save  
2、站点配置

    symbols_count_time:
      symbols: true
      time: true
      total_symbols: true
      total_time: true


##### 宠物

1、npm install --save hexo-helper-live2d  
2、[live2d插件](https://links.jianshu.com/go?to=https%3A%2F%2Fhuaji8.top%2Fpost%2Flive2d-plugin-2.0%2F)  
3、安装合适的宠物npm install live2d-widget-model-wanko  
4、在配置文件中添加即可

    live2d:
      enable: true
      scriptFrom: local
      pluginRootPath: live2dw/
      pluginJsPath: lib/
      pluginModelPath: assets/
      model:
    #    use: live2d-widget-model-tororo
    #    use: live2d-widget-model-hijiki
        use: live2d-widget-model-wanko
      display:
        position: right
        width: 150
        height: 300
    #    水平位置
    #    hOffset: 0
    #    垂直位置
    #    vOffset: -20
      mobile:
        show: true


##### 点击弹爱心

1、在source->js目录下新建一个js文件为click-love.js

    ! function (e, t, a) {
        function n() {
            c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"), o(), r()
        }
    
        function r() {
            for (var e = 0; e < d.length; e++) d[e].alpha <= 0 ? (t.body.removeChild(d[e].el), d.splice(e, 1)) : (d[e].y--, d[e].scale += .004, d[e].alpha -= .013, d[e].el.style.cssText = "left:" + d[e].x + "px;top:" + d[e].y + "px;opacity:" + d[e].alpha + ";transform:scale(" + d[e].scale + "," + d[e].scale + ") rotate(45deg);background:" + d[e].color + ";z-index:99999");
            requestAnimationFrame(r)
        }
    
        function o() {
            var t = "function" == typeof e.onclick && e.onclick;
            e.onclick = function (e) {
                t && t(), i(e)
            }
        }
    
        function i(e) {
            var a = t.createElement("div");
            a.className = "heart", d.push({
                el: a,
                x: e.clientX - 5,
                y: e.clientY - 5,
                scale: 1,
                alpha: 1,
                color: s()
            }), t.body.appendChild(a)
        }
    
        function c(e) {
            var a = t.createElement("style");
            a.type = "text/css";
            try {
                a.appendChild(t.createTextNode(e))
            } catch (t) {
                a.styleSheet.cssText = e
            }
            t.getElementsByTagName("head")[0].appendChild(a)
        }
    
        function s() {
            return "rgb(" + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + ")"
        }
        var d = [];
        e.requestAnimationFrame = function () {
            return e.requestAnimationFrame || e.webkitRequestAnimationFrame || e.mozRequestAnimationFrame || e.oRequestAnimationFrame || e.msRequestAnimationFrame || function (e) {
                setTimeout(e, 1e3 / 60)
            }
        }(), n()
    }(window, document);


2、在主题theme->layout->\_partials->footer文件中导入该js文件即可

    <script type="text/javascript" src="/js/click-love.js"></script>


2人点赞

[学习](https://www.jianshu.com/nb/27002944)

"小礼物走一走，来简书关注我"

赞赏支持还没有人赞赏，支持一下

[![  ](https://upload.jianshu.io/users/upload_avatars/4117703/d6b0133ae63b?imageMogr2/auto-orient/strip|imageView2/1/w/100/h/100/format/webp)](https://www.jianshu.com/u/3ef000cf53fb)

[汉娜爱吃TOMATO](https://www.jianshu.com/u/3ef000cf53fb "汉娜爱吃TOMATO")

总资产1 (约0.08元)共写了2017字获得2个赞共0个粉丝

关注