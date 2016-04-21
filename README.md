这是我最近用`hexo`搭建的个人博客,欢迎来参观留言,以下是我创建这个`hexo`的一步步步骤，欢迎指正!

　　**[我的博客](http://winterzhao.github.io/)**

　　参考自 [潘柏信的博客](http://leopardpan.github.io/2015/08/12/hexo/);[CnFeat](http://www.jianshu.com/p/05289a4bc8b2)

　　主题参考这里 [pacman](https://yangjian.me/pacman/hello/introducing-pacman-theme/);

　　主题选自这里 [hexadillax](https://github.com/XadillaX/hexadillax)


#### 1. 安装node;

#### 2. 安装git;

#### 3. 注册github账号;

#### 4. 新建文件夹'blog',进入`blog`,打开命令窗口。

　　4.1. `npm install hexo -g`;

　　4.2. `npm init`; (MIT协议);

　　4.3. `hexo init`;     //初始化

　　4.4. `hexo generate`  //配置静态文件;

　　4.5. `hexo server`      //启动服务 http://localhost:4000;

#### 5. 连接github.io

　　5.1. 建立repository: 仓库名为【username.github.io】,固定写法;

　　5.2. 修改_config.yml文件 【repo也可以SSH协议】

           deploy:
             type: git
             repo: git@github.com:winterZhao/winterZhao.github.io.git
             branch: master

　　5.3. ` npm install hexo-deployer-git --save `

　　5.4. `hexo deploy`  //另一种推送到github上的形式，**这时候访问winterZhao.github.io就可以了**

#### 6. 主题

[主题列表](https://github.com/hexojs/hexo/wiki/Themes),后头写有`demo`的为展示效果

我选择的是`Hexadillax`

　　6.1. 在blog目录下 `git clone git@github.com:XadillaX/hexadillax.git`将github上的文件copy到本地;

　　6.2. 将_config.sample.yml里的内容复制到根目录_config.yml里;修改`github`,我的为`winterZhao/winterZhao.github.io`;

　　6.3. 在source文件夹下新建文件夹`tags`,在其内新建`index.md`,写入内容:

```javascript
layout: tags
title: tags
---
```
　　6.4. 在source文件夹下新建文件夹`categories`,在其内新建`index.md`,写入内容:

```javascript
layout: categories
title: categories
---
```
 　　　　**注** : 默认没有采用`/tags`和`/categories`页面(标签和分类,需要的话执行6.3/6.4两步);

　　6.5. 将下载的Hexadillax文件夹整体复制到themes下;

　　6.6. 修改`_config.yml`里的`theme`为`hexadillax`;

　　6.7. 替换`source/images`下的`avatar`头像和`background`,名字不要改;

　　6.8. 替换`icon`图,在网站根目录以及`themes/hexadillax/source`下存放在网上生成的`favicon.ico`;

#### 7.添加百度统计

　　7.1. `_config.yml` 配置文件里添加`baidu_tongji:true`;
　　
　　7.2. 申请百度统计代码,复制统计代码到`themes/hexadillax/layout/partial`;　
　　
#### 8. 上传到github上，覆盖之前的;

　　8.1. `npm install hexo-deployer-git --save`;

　　8.2. `hexo deploy`;

　　**注**: 每次本地修改以后都要重复执行这两条命令;如果执行后没有效果，则按照`git`的流程进行
```javascript

git add -A;
git commit -m "提交";
git pull
git push -u origin master

```

#### 9. 安装爬虫插件;
　　9.1. `npm isntall hexo-generator-sitemap`; 

　　　　 `npm isntall hexo-generator-feed`;

　　9.2. 修改`_config.yml`,增加内容：

```javascript
# Extensions
Plugins:
- hexo-generator-feed
- hexo-generator-sitemap

#Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 20

#sitemap
sitemap:
  path: sitemap.xml


```
#### 10. 增加评论功能;

　　10.1. 注册多说账号;
　　
　　10.2. 在`_config.yml`里的`duoshuo`写上自己注册的多说账号;

#### 11. 写文章;
　　11.1. 命令窗口 `hexo clean`; //删除生成的文件和缓存

　　11.2. 命令窗口 `hexo new 文章名`;

　　11.3. 在`source/_posts`下找到对应的`md`文档，写markdown文章;

　　11.4. 命令窗口 `hexo generate`;   //生成静态文件到`public`下

　　11.5. 命令窗口 `hexo deploy`;   //推送到github上

   **注**:当我们`hexo deploy`的时候,会只将部分文件推送到github上，这是hexo默认的，不影响结构。
