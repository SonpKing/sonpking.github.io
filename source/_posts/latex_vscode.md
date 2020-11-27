---
title: VScode编写Latex文档
comments: true
categories: 工具
tags: [vscode]
date: 2020-11-27
---

## 软件安装
VScode > 1.50
Tex Live 2020
VScode插件：Latex Workshop, Latex Utilities(用于统计字数)

## 参数配置
在项目根目录创建.latexmkrc文件用于`latexmk`命令，内容如下
```sh
$out_dir="out";
$pdf_mode=5;
$xelatex="xelatex -outdir=out";
$xdvipdfmx="xdvipdfmx -q -E -o %D %O %S";
$clean_ext = 'thm bbl hd loe synctex.gz xdv run.xml';
$makeindex = 'makeindex -s gind.ist %O -o %D %S';
@default_files=('zjuthesis.tex')
```

在vscode setting.json文件下添加下面的配置，用于配合workshop插件
```json
"[latex]": {
    "editor.formatOnPaste": false,
    "editor.suggestSelection": "recentlyUsedByPrefix"
},
"latex-workshop.latex.tools": [
    {
        "name": "xelatex",
        "command": "xelatex",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-pdf",
            "%DOC%"
        ]
    },
    {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
        ]
    },
    {
        "name": "bibtex",
        "command": "biber", //这里配置的是实际调用的包
        "args": [
            "%DOCFILE%"
        ]
    }
],
"latex-workshop.latex.recipes": [ //这里的选项会出现插件中，方便点击使用
    {
        "name": "xelatex",
        "tools": [
            "xelatex"
        ]
    },
    {
        "name": "xe->bib->xe->xe",
        "tools": [
            "xelatex",
            "bibtex",
            "xelatex",
            "xelatex"
        ]
    }
],
"editor.wordWrap": "on", //编辑器自动换行
```

## 字体设置
在tex文件中加上如下配置，就可以自动根据系统选择合适的字体了
```latex
% ctex package stores one of "windows", "mac", and "fandol" in \g__ctex_fontset_tl
\ifthenelse{\equal{\csname g__ctex_fontset_tl\endcsname}{windows}}
{
    % Windows or other platform
    \setCJKmainfont[AutoFakeBold={\FakeBoldSize}]{SimSun}
}
{
    \IfFileExists{ /System/Library/Fonts/PingFang.ttc }
        {
            % MacOS El Capitan and later version
            % https://github.com/CTeX-org/ctex-kit/issues/351
            \setCJKmainfont[BoldFont={Songti SC Bold}]{Songti SC Light}
        }
        {
            % Older MacOS
            % Fonts
            \setCJKmainfont[AutoFakeBold={\FakeBoldSize}]{STSong}
        }
    }
}
```

## 编译过程
### 方法一
在根目录运行latexmk, 配置保存在.latexmkrc。
### 方法二
在workshop插件中先运行xelatex，再运行xe->bib->xe->xe编译参考文献
![](/images/posts/latex_vscode01.png)