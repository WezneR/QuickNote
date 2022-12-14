# QuickNote
 LaTeX 快速笔记

仅仅是用来记录一下自学过程，内容比较杂。

## 工作区配置
本工程中不包含LaTeX本体和LaTeX Workshop的配置信息，故在此文档中简要说明。

### LaTeX工具链
这里使用的是Texlive 2022提供的编译工具链，它应当在您的电脑上提前安装妥当，并正确添加名为`TEX`的系统环境变量。
### LaTeX Workshop 扩展的设置
这里将扩展配置放在VS Code全局用户设置(JSON)中。您也可以把它放在工作区设置文件`./vscode/settings.json`中。

```json
    "latex-workshop.latex.outDir": "%DIR%/build",
    "latex-workshop.latex.tools": [
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "--output-directory=%OUTDIR%",
                "%DOCFILE%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                // "--output-directory=%OUTDIR%",
                "%DOCFILE%"
            ]
        },
        {
            "name": "makeindex",
            "command": "makeindex",
            "args": [
                "%DOCFILE%.nlo",
                "-s",
                "nomencl.ist",
                "-o",
                "%DOCFILE%.nls"
            ]
        },
        {
            "name": "biber",
            "command": "biber",
            "args": [
                "%DOCFILE%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex🔃",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "xe->mkind->bib->xe*2🔃",
            "tools": [
                "xelatex",
                "makeindex",
                "biber",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "pdf->mkind->bib->pdf*2🔃",
            "tools": [
                "pdflatex",
                "makeindex",
                "biber",
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "xe->bib->xe->xe🔃",
            "tools": [
                "xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "biber🔃",
            "tools": [
                "biber"
            ]
        },
        {
            "name": "pdflatex🔃",
            "tools": [
                "pdflatex"
            ]
        },
        {
            "name": "pdf->bib->pdf->pdf🔃",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "BibTeX🔃",
            "tools": [
                "bibtex"
            ]
        }
    ],
    "latex-workshop.view.pdf.viewer": "external",
    "latex-workshop.view.pdf.ref.viewer":"external", 
    "latex-workshop.showContextMenu":true,
    "latex-workshop.view.pdf.external.viewer.command": "C:/Program Files/SumatraPDF/SumatraPDF.exe", 
    "latex-workshop.view.pdf.external.viewer.args": [
        "%PDF%"
    ],
    "latex-workshop.view.pdf.external.synctex.command": "C:/Program Files/SumatraPDF/SumatraPDF.exe", 
    "latex-workshop.view.pdf.external.synctex.args": [
        "-forward-search",
        "%TEX%",
        "%LINE%",
        "%PDF%"
    ],
    "latex-workshop.latex.recipe.default": "lastUsed",
    "latex-workshop.synctex.synctexjs.enabled": false,
    "latex-workshop.synctex.afterBuild.enabled": true,
```
注意，这份配置中包含了联动 *SumatraPDF* 实现正向搜索的功能，这不是必须的，如果需要，请更改`SumatraPDF.exe`的路径。


## 关于工程树格式

- `./build`是扩展配置中`"latex-workshop.latex.outDir"`一项所指定的工程输出目录。包含了中间件和PDF输出。
- `./figure`是手动存放所引用的图片的目录。
- `./code`是手动存放所引用的代码的目录。
- TeX源文件全部位于根目录下。
