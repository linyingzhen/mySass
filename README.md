sass -w style.scss:style.css --style expanded --sourcemap

sass -w style.scss:style.css --style compressed

sass -w style.sass:style.css --style expanded

sass -w style.sass:style.css --style compressed


# Convert Sass to SCSS
$ sass-convert style.sass style.scss

# Convert SCSS to Sass
$ sass-convert style.scss style.sass

――――――――――――――――――――――――――――――――――――――――――
Usage: sass [options] [INPUT] [OUTPUT]

Description:
  Converts SCSS or Sass files to CSS.

Common Options:
    -I, --load-path PATH             Specify a Sass import path.
    -r, --require LIB                Require a Ruby library before running Sass.

        --compass                    Make Compass imports available and load pro
ject configuration.
    -t, --style NAME                 Output style. Can be nested (default), comp
act, compressed, or expanded.
    -?, -h, --help                   Show this help message.
    -v, --version                    Print the Sass version.

Watching and Updating:
        --watch                      Watch files or directories for changes.
                                     The location of the generated CSS can be se
t using a colon:
                                       sass --watch input.sass:output.css
                                       sass --watch input-dir:output-dir
        --update                     Compile files or directories to CSS.
                                     Locations are set like --watch.
    -f, --force                      Recompile every Sass file, even if the CSS
file is newer.
                                     Only meaningful for --update.
        --stop-on-error              If a file fails to compile, exit immediatel
y.
                                     Only meaningful for --watch and --update.

Input and Output:
        --scss                       Use the CSS-superset SCSS syntax.
        --sourcemap=TYPE             How to link generated output to the source
files.
                                       auto (default): relative paths where poss
ible, file URIs elsewhere
                                       file: always absolute file URIs
                                       inline: include the source text in the so
urcemap
                                       none: no sourcemaps
    -s, --stdin                      Read input from standard input instead of a
n input file.
                                     This is the default if no input file is spe
cified.
    -E, --default-encoding ENCODING  Specify the default encoding for input file
s.
        --unix-newlines              Use Unix-style newlines in written files.
    -g, --debug-info                 Emit output that can be used by the FireSas
s Firebug plugin.
    -l, --line-numbers               Emit comments in the generated CSS indicati
ng the corresponding source line.
        --line-comments

Miscellaneous:
    -i, --interactive                Run an interactive SassScript shell.
    -c, --check                      Just check syntax, don't evaluate.
        --precision NUMBER_OF_DIGITS How many digits of precision to use when ou
tputting decimal numbers.
                                     Defaults to 10.
        --cache-location PATH        The path to save parsed Sass files. Default
s to .sass-cache.
    -C, --no-cache                   Don't cache parsed Sass files.
        --trace                      Show a full Ruby stack trace on error.
    -q, --quiet                      Silence warnings and status messages during
 compilation.

――――――――――――――――――――――――――――――――――――――――――




安装
安装Ruby
ruby -v
//如安装成功会打印
ruby 2.2.2p95 (2015-04-13 revision 50295) [i386-mingw32]
国内网络的问题导致gem源间歇性中断因此我们需要更换gem源
//1.删除原gem源
gem sources --remove https://rubygems.org/

//2.添加国内淘宝源
gem sources -a https://ruby.taobao.org/

//3.打印是否替换成功
gem sources -l

//4.更换成功后打印如下
*** CURRENT SOURCES ***
https://ruby.taobao.org/
安装Sass和Compass
//安装如下(如mac安装遇到权限问题需加 sudo gem install sass)
gem install sass
gem install compass
sass -v
compass -v

gem update sass
gem update compass

编译sass
sass编译有很多种方式，如命令行编译模式、sublime插件SASS-Build、编译软件koala、前端自动化软件codekit、Grunt打造前端自动化工作流grunt-sass、Gulp打造前端自动化工作流gulp-ruby-sass等。

命令行编译;
//单文件转换命令
sass input.scss output.css

//单文件监听命令
sass --watch input.scss:output.css

//如果你有很多的sass文件的目录，你也可以告诉sass监听整个目录：
sass --watch app/sass:public/stylesheets
命令行编译配置选项;
命令行编译sass有配置选项，如编译过后css排版、生成调试map、开启debug信息等，可通过使用命令sass -v查看详细。我们一般常用两种--style``--sourcemap。

//编译格式
sass --watch input.scss:output.css --style compact

//编译添加调试map
sass --watch input.scss:output.css --sourcemap

//选择编译格式并添加调试map
sass --watch input.scss:output.css --style expanded --sourcemap

//开启debug信息
sass --watch input.scss:output.css --debug-info
--style表示解析后的css是什么排版格式;
sass内置有四种编译格式:nested``expanded``compact``compressed。
--sourcemap表示开启sourcemap调试。开启sourcemap调试后，会生成一个后缀名为.css.map文件。
四种编译排版演示;
//未编译样式
.box {
  width: 300px;
  height: 400px;
  &-title {
    height: 30px;
    line-height: 30px;
  }
}
nested 编译排版格式
/*命令行内容*/
sass style.scss:style.css --style nested

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px; }
  .box-title {
    height: 30px;
    line-height: 30px; }
expanded 编译排版格式
/*命令行内容*/
sass style.scss:style.css --style expanded

/*编译过后样式*/
.box {
  width: 300px;
  height: 400px;
}
.box-title {
  height: 30px;
  line-height: 30px;
}
compact 编译排版格式
/*命令行内容*/
sass style.scss:style.css --style compact

/*编译过后样式*/
.box { width: 300px; height: 400px; }
.box-title { height: 30px; line-height: 30px; }
compressed 编译排版格式
/*命令行内容*/
sass style.scss:style.css --style compressed

/*编译过后样式*/
.box{width:300px;height:400px}.box-title{height:30px;line-height:30px}
软件方式编译;
这里推荐koala&codekit,它们是优秀的编译器，界面清晰简洁，操作起来也非常简单。鉴于koala是免费编译器，
