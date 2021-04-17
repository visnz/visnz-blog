# visn-video-blog

1. [关于OSS+CDN托管，Tag与Cat没有出现index.html问题的解决方案](https://github.com/iissnan/hexo-theme-next/issues/604)：
   1. 解决分类问题 replace [list_categories.js](./node_modules/hexo/lib/plugins/helper/list_categories.js) ``cat.path)}${suffix}">`;``->``cat.path)}index.html">`;``
   2. 解决词云问题 replace [tagcloud.js](./node_modules/hexo/lib/plugins/helper/tagcloud.js) ``tag.path)}${suffix}">`;``->``tag.path)}index.html">`;``
   3. Next Muse 用的tag模板不是hexo自带的[list_tags.js](./node_modules/hexo/lib/plugins/helper/list_tags.js)，而是自己写的在[post.swig](./themes/next/layout/_macro/post.swig)，replace ``{{ url_for(tag.path) }}``->``{{ url_for(tag.path) }}index.html``
