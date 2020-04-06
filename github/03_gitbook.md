# GitBook-Cli

工作的时候用gitbook-cli比较多，工作用的的git平台时gitlab，原生支持gitbook，gitbook也支持导出成PDF格式，另外配合VSCode的扩展`Markdown Preview Enhanced`，基本能满足日常技术文档的编写了。

Github不支持Gitbook生成器，可以现在本地build好静态网页后，再把_book中的文件push到project的gh-pages branch。

这里主要参考了以下文档：

* [Publish GitBook to Your GitHub Pages](http://sangsoonam.github.io/2016/08/02/publish-gitbook-to-your-github-pages.html)

* [how-to-gitbook](https://github.com/mitsuhisaT/how-to-gitbook)


## GitBook-Cli安装、使用、发布

1. `npm install -g gitbook-cli`

    这里记得把npm的源换成速度较快的淘宝镜像。

2. `gitbook init`

3. 使用VSCode + 扩展`Markdown Preview Enhanced` 进行编辑

4. `gitbook serve` 在本地做个预览

5. 发布到`project的gh-pages branch`

    下面列上可参考的版本，主要的目的就是把build好的_book目录中的文件copy到gh-pages branch的根目录，再push到Github。

    ```
    # install the plugins and build the static site
    gitbook install && gitbook build

    # checkout to the gh-pages branch
    git checkout gh-pages

    # pull the latest updates
    git pull origin gh-pages --rebase

    # copy the static site files into the current directory.
    cp -R _book/* .

    # remove 'node_modules' and '_book' directory
    git clean -fx node_modules
    git clean -fx _book

    # add all files
    git add .

    # commit
    git commit -a -m "Update docs"

    # push to the origin
    git push origin gh-pages

    # checkout to the master branch
    git checkout master
    ```