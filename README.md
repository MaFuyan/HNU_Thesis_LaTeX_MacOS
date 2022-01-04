# 湖南大学硕士学位论文 LaTeX 模板 MacOS适配

本项目基于[Gwinel](https://github.com/Gwinel/Latex/)，进行MacOS下的适配和安装说明


## 配置MacOS下的LaTeX和VSCode

1. 下载并安装[MacTex](https://www.tug.org/mactex/mactex-download.html)和[VSCode](https://code.visualstudio.com).
2. 在VSCode的Extensions里安装LaTeX Workshop。
3. 在VSCode的配置json文件中，添加下面的配置代码<details>
   <summary>配置代码</summary>

   ```json
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
       "name": "latexmk",
       "command": "latexmk",
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
       "command": "bibtex",
       "args": [
         "%DOCFILE%"
       ]
     },
     {
       "name": "biber",
       "command": "biber",
       "args": [
         "%DOCFILE%"
       ]
     }
   ],
   "latex-workshop.latex.recipes": [
    {
      "name": "xelatex -> biber -> xelatex*2",
      "tools": [
        "xelatex",
        "biber",
        "xelatex",
        "xelatex"
      ]
    },
    {
      "name": "xelatex -> bibtex -> xelatex*2",
      "tools": [
        "xelatex",
        "bibtex",
        "xelatex",
        "xelatex"
      ]
    },
     {
       "name": "xelatex",
       "tools": [
         "xelatex"
       ]
     },
   ],
   "editor.wordWrap": "on",
   "latex-workshop.view.pdf.viewer": "tab"
   ```
   </details>
4. clone此项目到本地
    ```
    git clone https://github.com/MaFuyan/HNU_Thesis_LaTex_MacOS.git
    ```
5. 进行编译和预览即可


## 关键文件说明
------------
* `main.tex`:主文件，编译入口
* `hnuthesis.cls`:撰写规范，需要调整格式在该文件中对应修改
* `chapters/`:论文章节文件夹，分章有利于保持tex文件的整洁
* `figures/`:插图文件夹，latex支持多种格式，如eps,png,jpg,pdf等
* `main.pdf`:根据你的tex文件编译生成的论文草稿

## 修改说明

原项目无法直接在MacOS下运行的原因是原始版本的 **hnuthesis.cls** 是在windows平台进行开发的，而MacOS下的字体不对应，导致编译时会报The font xxx cannot be found的错。

在**hnuthesis.cls**中修改字体对应关系如下：
```latex
\setCJKmainfont[BoldFont=STHeiti , ItalicFont = STKaiti ]{STSong}
\setCJKsansfont{STHeiti}
\setCJKmonofont{STFangsong}
\setCJKfamilyfont{zhsong}{STSong}
\setCJKfamilyfont{zhhei}{STHeiti}
\setCJKfamilyfont{zhkai}{STKaiti}
\setCJKfamilyfont{zhfs}{STFangsong}
```

如果有bug存在，欢迎提出issue修改，也可联系 mafuyan@hnu.edu.cn