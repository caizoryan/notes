# Lets 5ee

### Buffer functions
```
;; will insert 'string' in current buffer
(insert "something")

(progn
	;; create a new buffer with name
	(setq xbuff (generate-new-buffer "*testing*"))

	;; print to a buffer
	(prin1 "something" xbuff)

	;; switch to a buffer
	(switch-to-buffer xbuff )
		
	;; insert at current point
	(insert "something more than this"))
```


### Making Child frames

```
(progn
(make-frame (
	list
		(cons 'minibuffer nil)

		;; making child frame
		(cons 'parent-frame (selected-frame))
		(cons 'width 50)
		(cons 'height 20)
		(cons 'border-color "#ffffff")
		(cons 'drag-with-mode-line t)
		(cons 'border-width 2)
		(cons 'left 850)
		(cons 'top 450)))
		(switch-to-buffer "todo.md"))
```


### Deleteing and switching to frames
```
(delete-frame)
(delete-frame (nth 0 (frame-list)))
(select-frame-set-input-focus (nth 0 (frame-list)))
(select-frame-set-input-focus (nth 1 (frame-list)))
(select-frame-set-input-focus (nth 2 (frame-list)))
```
