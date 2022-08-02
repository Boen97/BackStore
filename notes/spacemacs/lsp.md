## lsp intall location
`.emacs.d/.cache/lsp`

## manual let lsp import project
`M-x` lsp
i

## lsp initialized with wrong project path
1. delete /Users/rhyme/.emacs.d/.cache/lsp/.lsp-session-v1
2. `M-x` lsp
3. i reimport the project

## change jdt update url
customize variable `lsp-java-jdt-download-url`

## quick insert lsp-mode snippets
SPC i s

## run go
, x x

## enable Scala mill build tool

1. cd ~/.emacs.d/layers/+lang/scala
2. init-scala-mode
```lisp
(defun scala/init-scala-mode ()
  (use-package scala-mode
    :defer t
    :mode "\\.sc\\'"
    ...
```
