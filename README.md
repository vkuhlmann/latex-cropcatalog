# LaTeX cropcatalog

This LaTeX package allows you to designate zones of interest in a pdf. You can use the package again in another LaTeX file to generate a pdf cropped to a specific zone.
This can for example be handy when storing a lot of images or tables in your pdf. Whenever you want a specific part, this package can easily retrieve it.

Currently does not support nesting of zones. The package is missing some features. If the package is a success, these will likely be added.

This package is in response to a question at: https://tex.stackexchange.com/questions/598138/mac-mactextexshoppreview-fine-pdf-cropping-turns-out-blurry-on-windows

# Installation

Currently, the package isn't available at CTAN. Copy the `.sty` file to the same directory as the `.tex` files where you want to use it in. Or, copy the text contents,
paste them in your text editor, and save them using the `.sty` extension, in the directory mentioned.

# Use

For your source file:
```latex
\documentclass[a4paper]{article}
\usepackage{graphicx}

% Use '\usepackage[nocropframe]{cropcatalog}' to disable the cropframe
\usepackage{cropcatalog}

\begin{document}
    Can you \cropbox{crop me \includegraphics[width=5cm]{example-image-a}?}
    
    \cropbox{And me? \includegraphics[height=1cm]{example-image-b}}
\end{document}
```
use `\cropbox` around a zone of interest.

For your extract file:
```latex
\documentclass{article}

\usepackage[
    source={document.pdf},
    catalog={document_cropcatalog.txt}
]{cropcatalog}

\begin{document}
    \extractAsPage{1}

    Some normal page!\extractAsGraphic{2} with an image\hfill

    \extractAsPage{2}
    \extractAsPage{1}
\end{document}
```
where we assume the source file was `document.tex` which generated `document.pdf` and the auxiliary file `document_cropcatalog.txt`.

To have the extraction be only one page, just use a single `\extractAsPage{...}` as the only contents of the `document`-environment.
