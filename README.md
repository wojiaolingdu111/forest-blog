# ForestBlog

> ForestBlog 是基于 go 语言开发的，不依赖第三方 go 库，适合用来学习和展示 markdown 文档的精美博客。


:chestnut:  [xusenlin.com](http://xusenlin.com) （个人博客，正在使用）

:point_right:  [github.com/xusenlin/ForestBlog](https://github.com/xusenlin/ForestBlog)

---  

## 项目背景
博客从最早的静态 Html+Css 主页到 Wordpress 、Typecho 、Hexo 、Hugo 一路尝试过来，虽然他们都是很优秀的开源项目，但是没有一款符合我内心真正的诉求。
他们有的要么太重了要么部署不方便要么对存储的文章不友好，我就放弃了之前在Typecho上的文章，同时调整分类也不那么灵活，有的迁移也不方便。
自己太懒，不想自己做文章备份，不想安装数据库，快速响应也是必须的，所以才有了用 GOLANG 来写一个简单博客的想法。
当然，自己的这个项目并不能和这些优秀的开源项目相比较，它只是符合我自己的诉求顺便用来学习GOLANG的项目。(写文章也能增加github的活跃度，逃 :))

## ForestBlog 在做什么


简单来说，ForestBlog 会使用 git 将你的 .md 文档仓库克隆到当前目录下, 然后并行加载和解析文章关键信息并生成内容，呈现一个博客站点。
当你向你的 git 仓库提交文章的时候，你可以设置 webHooks 来自动通知 ForestBlog 更新同步文章，或者可以在仪表盘里手动更新文章。


## 安装
你可以克隆当前仓库，然后在 JSON 文件里面配置好你文档的 Git 地址和 WebHook 秘钥，编译源代码并放入后台运行。


## 使用

- 配置好 config.json 文件，详细的配置说明文件在当前仓库根目录的《配置说明.md》
- 新建一个 git 仓库，用来存放你的文章，但是对你的目录结构有一些要求
如下：
```
    |-- assets       //博客静态文件，存放一些图片资源，方便显示到文档里
    |-- content
    |   |-- GOLANG   //分类目录
    |       |-- GOLANG基础   //  子分类目录，但是在页面上不会产生分类目录
    |       |--- GOLANG基础语法.md   
    |   |-- 其他分类
    |       |--- xxx.md
    |-- extra_nav  // ForestBlog只会有 Blog Categories 两个导航，其他导航可以放到这个目录下，比如自己的简历，作品之类的
    
```
content目录下的一级目录代表一个分类，如果一级目录下有子级目录也不会产生新的分类,子级目录的文档也会属于一级目录的分类。

- 每一篇文章的开头可以配置一些文章的属性，具体可以看 配置说明.md
如下：
```
    ```json
    {
        "date":"2019.01.02 14:33"，//最少需要
        "tags": ["BLOG"，"其它tag"]，//可以不填，不过最好添加一些tag，后面可以做一些好玩的东西。
        "title": "文章的标题，一般不用填写，默认使用文件名"，
        "description": "文章描述，不填写自动取正文200个字，可以在app.json中配置"，
        "author": "xusenlin"， //文章作者，可以不用填写，现在也没有使用到
        "musicId":"网易云的音乐ID" //文章的配歌
    }
    ```
```
我会根据关键字```json来解析，不用担心这个会显示到文章内容里面，我在解析的时候就将它去掉了。
如果不再文章前面添加这一段json也是可以的，不过我不建议这么做，因为这样就和V1.0版本没什么区别了，没有了文章属性，排序都是个问题。
最后，mac markdown 文章编辑器推荐 Typora。

> 提示：```json 前面不能有其它字符。

- 切换主题色和搜索文章在仪表盘里，访问/admin 可以查看仪表盘，
如果不想让别人知道你的仪表盘地址可以自己配置dashboardEntrance字段。


## TODO
- [x] 1.移动端更好的适配
- [x] 2.根目录可以添加其他文件生成导航
- [x] 3.仪表盘支持切换主题色
- [x] 4.仪表盘支持搜索
- [ ] 5.tags的展示
- [x] 6.仪表盘添加手动更新文章功能
- [x] 7.添加webHook支持(去掉自动更新)
- [x] 8.添加评论支持(在配置里开启，所有评论都会储存在仓库的Issues)
- [x] 9.支持网易云音乐
- [ ] 10.支持自定义切换主题

> 后续尽善尽美之后，我可能会提供其他漂亮的主题皮肤，也欢迎大家参与进来。

## 特性

1. 响应迅速  ---没有什么依赖，得益于GOLANG的运行速度，部署在阿里云的博客平均响应在50毫秒内。
2. 迁移方便  ---GOLANG交叉编译可以方便的发布二进制文件到不同的操作系统，执行二进制文件并克隆博客文件即可运行你的博客。
3. 小巧精美  ---非常简单的代码方便学习和改造，即使有一天你厌倦ForestBlog，你的文章也能很好的迁移和阅读。
4. 分类调整  ---随时调整你的文章分类，你可以把一个文件夹里所有的东西移动到其他分类里的某个地方，不管有多少层级，分类发生了什么翻天覆地的变化，下一次更新就能展示。

## 更新日志
### V3.1 未发布
* 去掉标题的.MD后缀
* 添加文档图片移动到网站根目录images下，本地写文章时可以使用 ```![demo](./images/demo.jpg)```连接图片，线上自动连接。

### V3.0
* 完全重构，添加了短链，美化了 URL 
* 自动完成克隆工作
* 添加了网易云音乐功能
* 文件自动生成导航（导航排序通过时间可自定义）

### V2.0
* 文章可以配置一些关键信息，可排序
* 添加仪表盘
* 添加文章评论
* 支持切换主题
* 移动端更好的适配
* 添加webHook支持

### V1.0
* 基础功能，手动克隆并定时更新文章


##  感谢
<a href="https://www.jetbrains.com/?from=ForestBlog"><img src="resources/images/jetbrains.png" width="100" alt="JetBrains"/></a>

## License

MIT © Richard McRichface
