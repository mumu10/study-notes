# GitHub Pages

GitHub Page的帮助文档还是看官方的帮助文档比较清楚，其中容易忽略的是Pages Sites的种类和它们各自对应的默认域名以及默认发布Branch的官方说明。

另外，GitHub Pages的静态网页生成只支持Jekyll。Jekyll基于Ruby，墙内Windows环境安装比较坑人；另外，Jekyll的Liquid标记没有很好的所见即所得的编辑器支持，感觉不是很好的选择。

因此至少对我而言，project类型的GitHub Pages还是使用GitBook Build完静态网页后，再发布到GitHub比较好。

## Types of GitHub Pages sites

* project
    `http(s)://<user>.github.io/<repository>` or `http(s)://<organization>.github.io/<repository>`.
* user
    `<user>.github.io`
* organization
    `<organization>.github.io`

## Publishing sources for GitHub Pages sites

The default publishing source for user and organization sites is the master branch. 

The default publishing source for a project site is the gh-pages branch. If the repository for your project site has a gh-pages branch, your site will publish automatically from that branch.

Project sites can also be published from the master branch or a /docs folder on the master branch. 

## Static site generators

GitHub Pages publishes any static files that you push to your repository. You can create your own static files or use a static site generator to build your site for you. You can also customize your own build process locally or on another server. We recommend Jekyll, a static site generator with built-in support for GitHub Pages and a simplified build process. 

GitHub Pages will use Jekyll to build your site by default. If you want to use a static site generator other than Jekyll, disable the Jekyll build process by creating an empty file called .nojekyll in the root of your publishing source, then follow your static site generator's instructions to build your site locally.