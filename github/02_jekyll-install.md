# Jekyll Install

不是很清楚为什么Github Pages的网页生成器只支持Jekyll，Ruby在国内也就火了那么一下，现在的流行程度并不高，因此相关的材料并不多。

## Jekyll on Windows

在Windows上安装Jekyll有两种方案：
* Installation via RubyInstaller
* Windows Subsystem for Linux (WSL)

WSL现在有1.0和2.0两个版本，1.0版本必须装在C盘，2.0盘也必须升级Win10，对我而言都不合适，因此选择直接在Win10上安装RubyInstaller。

1. Download and Install a Ruby+Devkit version from RubyInstaller Downloads. Use default options for installation.

    * 这里就遇到一个挑战，官方的RubyInstaller Downloads非常的慢，可以预见不翻墙的情况下，几乎不可能下载成功。国内的Ruby社区[Ruby China](https://ruby-china.org/)也没有Windows安装包的下载。CSDN上倒是有2.6.5版本的下载，但是都要积分。只好从公司下载完后把安装包拷贝回家安装。

2. Run the ridk install step on the last stage of the installation wizard. This is needed for installing gems with native extensions. You can find additional information regarding this in the RubyInstaller Documentation

3. Open a new command prompt window from the start menu, so that changes to the PATH environment variable becomes effective. Install Jekyll and Bundler via: `gem install jekyll bundler`

    * 在这一步，倒是没有碰到gem install非常慢的问题，如果遇到也可以在这一步修改Ruby的gem source源到Ruby China。

4. Check if Jekyll installed properly: `jekyll -v`

## Create a new Jekyll site on Github Pages user site

1. clone `<user>.github.io` 项目，进入项目的master branch的根目录，运行如下命令创建新的Jekyll site：
    ```
    jekyll new .
    ```
    如果在Github网页上创建`<user>.github.io` 项目时，已经选择了theme等，根目录已经存在文件了，根据提示加上`--force`即可。

2. Build the site and make it available on a local server.
    `bundle exec jekyll serve`
    
    jekyll运行采用了bundle的方式，这个时候就会遇到gem下载非常慢的问题，可以通过两种方式解决：
    * 修改gem source，然后按照`Gemfile`的依赖，一个一个的gem包安装。
    * 直接修改`Gemfile`第一行source会更加方便。
    
    我是按照第一个方式做的，中间碰到`TZInfo 2.0 incompatibility`的问题，困扰了很久，尝试多次，最后通过`gem install tzinfo -v 1.2`指定安装版本才解决。后来才发现在Jekyll的安装说明[Jekyll on Windows](https://jekyllrb.com/docs/installation/windows/)的后半部分有个很明显的提醒：
    
    <span style="background:red;">
    TZInfo 2.0 incompatibility
    Version 2.0 of the TZInfo library has introduced a change in how timezone offsets are calculated. This will result in incorrect date and time for your posts when the site is built with Jekyll 3.x on Windows.
    We therefore recommend that you lock the Timezone library to version 1.2 and above by listing gem 'tzinfo', '~> 1.2' in your Gemfile.
    </span>
    
    


