以下是我的Sublime Text 3 配置  

## 1.Package Control
Sublime包管理工具，必装
ctrl+` 打开控制台，输入以下代码  
```
import urllib2,os; pf=’Package Control.sublime-package’; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler( ))); open( os.path.join( ipp, pf), ‘wb’ ).write( urllib2.urlopen( ‘http://sublime.wbond.net/’ +pf.replace( ‘ ‘,’%20′ )).read()); print( ‘Please restart Sublime Text to finish installation’)
```

## 2. Emmet
Zen Coding，不多解释，懂得自然懂，虽然Sublime3 原生提供了部分Emmet语法，但是不全，比如 html:5 就没有  
###修改 Emmet 兼容jsx 文件
打开 `preferences -> Key bindings - Users`，把下面代码复制到[]内部
``` json
{
  "keys": [
    "super+e"
  ],
  "args": {
    "action": "expand_abbreviation"
  },
  "command": "run_emmet_action",
  "context": [{
    "key": "emmet_action_enabled.expand_abbreviation"
  }]
},
{
  "keys": ["tab"],
  "command": "expand_abbreviation_by_tab",
  "context": [{
    "operand": "source.js",
    "operator": "equal",
    "match_all": true,
    "key": "selector"
  }, {
    "key": "preceding_text",
    "operator": "regex_contains",
    "operand": "(\\b(a\\b|div|span|p\\b|button)(\\.\\w*|>\\w*)?([^}]*?}$)?)",
    "match_all": true
  }, {
    "key": "selection_empty",
    "operator": "equal",
    "operand": true,
    "match_all": true
  }]
}
```

## 3.EditorConfig
代码格式管家，最主要的功能是，同一项目代码在不同编辑器下能够保持统一的代码风格（主要是缩进，如sublime默认缩进宽度是4，我写JS缩进都是2）。
EditorConfig支持除Sublime之外的很多主流编辑器与IDE，如VisualStudio, Eclipse, VIM, WebStorm等
### 使用：
在项目根目录新建一个文件：.editorconfig，在此文件里填写你需要的格式规则，以下是一个典型的.editorconfig
``` xml
# http://editorconfig.org
 
root = true
 
[*]
# Change these settings to your own preference
indent_style = space
indent_size = 2
 
# We recommend you to keep these unchanged
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
 
[*.md]
trim_trailing_whitespace = false
```

## 4. JSHint Gutter
JSHint不但能检查JS代码的语法错误，还能够监控代码质量（风格），很多公司跟开源项目都在使用它，比如：Facebook、jQuery、Bootstrap等等。在Github上，使用JSHint的项目多如牛毛，如果你在某个项目里面，发现有.jshintrc文件，那它就使用了JSHint。JSHint是一个独立的工具，它不直接提供对Sublime的支持，它本身只提供基于NodeJS的命令行工具。而JSHint Gutter这个插件，它能够调用JSHint的命令行工具，执行代码检查并将结果显示到Sublime界面上。  
### 安装JSHint
先安装好NodeJS，然后在终端/命令行中输入 npm install -g jshint  
### 安装与配置JSHint Gutter
安装打开
``` bash
Preference->Package Settings->JSHint Gutter->Set 'node' Path
```
设置NodeJS执行文件所在的路径（node_path），并将lint_on_save（文件保存时检查）选项设为 true
### 设置.jshintrc
在项目根目录新建一个文件：.jshintrc，在此文件里填写你的检查规则，以下是一个典型的.jshintrc
``` js
{
  "curly": true,
  "eqeqeq": true,
  "immed": true,
  "noarg": true,
  "noempty": true,
  "quotmark": "single",
  "undef": true,
  "unused": true,
  "node": true
}
```
第二行：curly 表示所有的代码块必须使用大括号  
第三行：eqeqeq 表示判断相等时，必须使用 ===  
第四行：immed 表示立即执行函数必须用括号包起来 `(function () { } ());`  
第五行：noarg 表示禁止使用 `arguments.caller` 和 `arguments.callee`  
第六行：noempty 表示禁止出现空的代码块 `{ }`  
第七行：quotmark 是引号的使用规则，有以下四个选项  
false : 不检查  
true : 检查一致性（要么都是单引号，要么都是双引号）  
single : 必须都是单引号  
double : 必须都是双引号  

## 5. Bracket​Highlighter
括号高亮匹配，眼睛不好

## 6. Js​Format
JavaScript 代码格式化插件，快捷键是 ctrl+alt+f

## 7. Color​Picker
跨平台取色器插件，快捷键 ctrl+shift+c

## 8. Color Highlighter
CSS中的颜色可以实时看到什么颜色

## 9. TrailingSpacer
高亮显示多余的空格和Tab，在保存文件的时候自动删除他们，代码洁癖

## 9. Babel
支持ES6， React.js, jsx代码高亮，对 JavaScript, jQuery 也有很好的扩展  
### 配置
打开.js, .jsx 后缀的文件;
打开菜单`view， Syntax -> Open all with current extension as... -> Babel -> JavaScript (Babel)`，选择babel为默认 javascript 打开syntax

## ****添加右键菜单****
绿色便携版没有右键 Edit with sublime 得写注册表，我参考了网上，用ActiveX JS写了个网页脚本，用管理员权限打开IE浏览器运行这个网页  
先在input框里选择你的 sublime_text.exe文件，主要是获取你的sublime文件路径，其实ActiveX里有个api是WshShell.CurrentDirectory获取当前路径，不知道为什么运行后永远是桌面路径，暂时没找到解决方法，只能退而求其次自己选择路径了  
看按钮名就知道功能了，添加右键菜单的注册表和删除右键菜单的注册表

> 暂时先这些，如有改动我会及时更新
