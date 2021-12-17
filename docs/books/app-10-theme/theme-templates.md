## 模板文件及缺省机制

- 因为「保留模板」机制，当主题未提供某一模板文件时，系统会从`zb_system/defend/default`中读取使用；「[在线查看](https://github1s.com/zblogcn/zblogphp/blob/HEAD/zb_system/defend/default/index.php "zb_system/defend/default")」
- 因此可以缺省部分不需要自定义内容结构的模板文件，尤其是「[侧栏模块相关](books/dev-10-theme?id=侧栏模块相关模板 "侧栏模块相关")」的部分；

### 页面公共模板文件

| 模板文件   | 说明         |
| ---------- | ------------ |
| header.php | 公共头部文件 |
| footer.php | 公共尾部文件 |


### 首页与列表页相关模板

| 模板文件       | 说明                   |
| -------------- | ---------------------- |
| index.php      | 首页及列表页主模板文件 |
| post-multi.php | 摘要文章模板           |
| post-istop.php | 置顶文章模板           |
| pagebar.php    | 页码模板               |

### 日志/独立页相关模板

| 模板文件               | 说明                       |
| ---------------------- | -------------------------- |
| single.php             | 文章页(单页)主模板文件     |
| post-single.php        | 日志页文章模板             |
| post-page.php          | 独立页面模板               |
| comments.php            | 评论区模板                 |
| comment.php           | 每条评论内容显示模板       |
| commentpost.php        | 评论发送表单模板           |
| commentpost-verify.php | 评论验证码模板（1.5 新增） |

###  侧栏模块相关模板
- 模块展现外框架模板

| 模板文件    | 说明                                                                   |
| ----------- | ---------------------------------------------------------------------- |
| sidebar.php | 默认侧栏模板，可自定义 `sidebar2.php`~`sidebar9.php` 用于后续侧栏调用  |
| module.php  | 模块显示模板，可定义模块标题等格式，模块具体内容格式由下列细节模板决定 |

- 模块内容细节模板（1.5 版本及以上）

| 模板文件              | 说明             | 备注（默认列表行数） |
| --------------------- | ---------------- | -------------------- |
| module-archives.php   | 文章归档模块     | 没有限制             |
| module-authors.php    | 作者列表模块     | 没有限制             |
| module-calendar.php   | 日历模块         | 没有限制             |
| module-catalog.php    | 分类列表模块     | 没有限制             |
| module-navbar.php     | 导航条模块       | 没有限制             |
| module-statistics.php | 站点信息模块     | 没有限制             |
| module-comments.php   | 最近评论列表模块 | **10**条             |
| module-previous.php   | 最近文章列表模块 | **10**条             |
| module-tags.php       | 标签列表模块     | **25**条             |
