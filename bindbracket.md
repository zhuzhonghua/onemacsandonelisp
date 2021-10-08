绑定左括号和右括号

当按下 ( 时，判断当前(point)之前的字符是啥，如果是 ) 则执行 (backward-sexp)

```lisp
(defun me-left-bracket-bind ()
	"when press ("
	(interactive)
	(if (equal ?\) (char-before (point)))
			(backward-sexp)))
```

使用 char-before 获取当前字符前面的字符，然后使用(equal)比较 ?\\)

```lisp
(define-key me-local-mode-map (kbd "(") 'me-left-bracket-bind)
```

再绑定对应key

同理，当按下 ) 时，判断 (point) 之后的字符，如果是 ( 则执行 (forward-sexp)

```lisp
(defun me-right-bracket-bind ()
	"when press )"
	(interactive)
	(if (equal ?\( (char-after (point)))
			(forward-sexp)))
```

使用 char-after 获取当前字符后面的字符，然后使用(equal)比较 ?\\(

```lisp
(define-key me-local-mode-map (kbd ")") 'me-right-bracket-bind)
```



还可以向后或者向前找到 ( 或者 ) ，然后再执行(forward-sexp) 或者 (backward-sexp)

也可以除了左右括号 ()，还可以匹配中括号 []，大括号 {} 等等

除了可以执行(forward-sexp) 或者 (backward-sexp)之外，可以根据自己需要执行其他动作