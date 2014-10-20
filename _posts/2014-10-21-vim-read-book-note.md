---
layout: page
title: "vim读书笔记"
categories:
- tools vim
tags:
- tools
---

###vim笔记


----
以前整理过vim的读书笔记，是印度一位很有天赋的骚年骚写骚的骚一本骚书。
写了些常用的使用技巧，不像vim  用户手册那么大而全，非常适合用户自己
日常工作的使用，以下指令就可以高效完成90%的文本编辑工作了。
当然只是一些速记笔记，掌握vim的人可以时不时翻一下，以便回忆起一些
很久没用到有点生疏的指令
----
==============================
Normal mode

:x   save working files and quit
:wq 
 ZZ 
 :qa   Exit all open files
 :version
 vimtutor
 [Ctrl] +  F
 [Ctrl]  + B
 [Ctrl]  + E
 [Ctrl]   +  Y

 jump :w  W  e  E  b B 
 {
 } 
 ( 
 )
 [[ 
 ]]

 H  M   L  (screen  jump)


 50% (Go to the 50th percentage of file)
 :50   (Go to the 50 th  line)
 50gg   (Another way to jump to 50 th line)


 [(  (Go to the previous unmatched (    )
 [])   (Go to the previous unmatched  )    )
 [{    (Go to the previous unmatched  {    })
 []}     (Go to the previous unmatched  )]]   )


 [Ctrl]  + O (jump back to previous spot)
 [Ctrl]   + I   (jump forward to next spot)



----
 vim +?search-term  filename   (Go to the first of the specified search term from bottom)
 vim +/search-term  filename   (Go to the frist of the specified search term from top)
 vim -t TAG  (Go to specific tag)



----
 marks:
 ma
 `a
 'a
 :marks
 
 ma,mb,then  :'a,'bs/old/new/gc
 will display specific area  word
 
 
 
 `"  (To the position where you did last edit before exit)
 '.  (To the position of where the last change was made)
 
 
 
 ddp  dwp  
 
 
 
 
 :r!   COMMAND (Insert output of a command into current file after the current line)
 ==================================
 Insert Mode
 SHIFT-<Right  Arrow>  Go to right word -by-word  in insert mode
 SHIFT-<Right  Arrow>  Go to left word-by-word  in insert mode
 
----
 =========================================
 copy line to the clipboard
 
 :%y+
 :y+
 :N,My+
 
 To copy the visual selected line to the clipboard,first visually select the
 lines, and :y+ which will apppear as :'<,'>y+
 
 here please check if your vim version support y+　register
 
 
 
----
 ========================================
 write part of File to another File
 
 visual mode selected save area,  then :
 :w newfilename
 
 also you can do like this:
 :5,10w  newfilename
 
 
 ===================================
 swap line or character
 
 :xp   (swap character)
 :ddp  (swap line)
 
 
 
 ==================================
 (dot)  usage:
 1. Search for a string in a file using: /zhihao
 2. Replace zhihao with wzhihao  using: cwwzhihao<Esc>
 3.Search for the next occurrence of zhihao:n
 4.Replace zhihao with wzhihao using:.(dot)
 
 
 
 ==================================
 :g usage
 :g/^$/d  (delete all empty lines in the file)
 :g/^\s*$/d  (delete all  empty  and blank lines in the file)
 :g/pattern/d  (delete )
 :g/pattern/. w >> filename  (Extract line with specific pattern and write it into another file)(very userful!!!)
 :g/^/m0  (reverse a file)
 
 :g/^\s*PATTERN\exe "norm! |/*\<ESC>A*/\<ESC>"  (Add a C style comment {/*text */} to all lines matching the pattern)
 (it can not work in gvim  yet,though it seems to be so useful  ~~~~)
 
 =====================================
 Copy Lines to Named Buffer for Later Use
 valid named buffer: a to z (26 total valid named buffers)
 
 "ayy
 "a5yy  (copied 5 lines to buffer "a")
 "ap  (Paste copied lines from buffer "a"  after the cursor)
 "aP  (Paste copied lines from buffer "a"   before the cursor)
 
 
 
----
 ====================================
 lowcase to uppercase,normally used in header file define
 visual mode 
 select replace area
 U  (to upper case)
 u   (to lower case)
 
 
 
 
 
----
 ================================
 sort file content from vim as below
 :sort 
 
 sort selected content
 visual mode select specific area and add !sort at the end
 :'<,'>!sort
 
 :sort !  (descending order)
 :sort i (sort ignore case)
 :sort u (remove duplicate lines)
 
 
 
----
 ====================================
 
 Extremely useful!  (78)
 
 create a new *.c  file with automatic header
 
 cat  c_header.txt
 :insert
 
 /*-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.
 
 *        File  Name:
 *
 *        Purpose:
 *
 *        Creation Date:
 *
 *        Last Modified:
 *
 *        Created By :
 *
 -.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.*/
 
 add following lines in ~/.vimrc  file
 
 autocmd bufnewfile *.c  so  /chriswei/c_header.txt
 autocmd bufnewfile *.c  exe "1," . 10 . "g/File  Name : .*/s//FileName
 : " .expand(%s)
 autocmd  bufnewfile *.c  exe "1,"  .10 . "g/Creation Date :.*/s//Cteation Date:
  " .strftime("%d-%m-%Y")
  autocmd Bufwritepre,filewritepre  *.c  execute "normal ma"
  autocmd  Bufwritepre ,filewritepre *.c exe "1," . 10.
  "g/Last Modified:.*/s/Last Modified:.*/Last Modified:" .strftime(%c)
  autocmd bufwritepost,filewritepost *.c execute "normal `a"
  
  
  =====================================
  editor  color 
  :syn on
  :syn off
  
  =====================================
  (extremely useful!)
  in vim Press K  on the word for which you want to read the man
  page
  K
  
  
  ======================================
  (extremely useful!)
  gd  (Go to the local declaration of a variable)
  
  gD (Go to the global declaration of a variable)
  
  
  
  
  =====================================
  (extremely useful)
  [Ctrl]  -  A  (incre Number)
  [Ctrl]  -  X   (Desc Number)
  
  
  ====================================
  (extremely useful!)
  to execute single Vim command  in insert mode
  
  [Ctrl]  +　Ｏ
  
  you are in insert mode typing characters
  Press  Ctrl - O ,which will terporarily take you to command mode
  do some vim command
  then you will automatically back in insert mode after the single vim commands is executed
  
  [Ctrl]  +  G  view file details
  
  
  
----
  gUU  change all the visual selected area to uppercase
  guu change all the visual selected area to lowercase
  =====================================
  
  execute any vim command when opening a file
  
  vim -c '<command   1>'  -c '<command 2>'  <filename>
  
  ======================================
  skip loading plugins temporarily
  vim --noplugin filename.txt
  
  
  ====================================
  change color scheme
  
  :colorsheme  [color scheme]
  
  
  ===================================
  (extremely useful!)
  gf  (open a file whose names is currently under the cursor)
  
  
  ===================================
  (safe   encrypt  extremely useful)
  :X
  
  unencrypt
  :set key = 
  (to remove encrypt key)
  
  ===================================
  (extremely useful)
  save and resume vim sessions
  :mksession  filename
  
  vim -S filename
  
----
  ====================================
  
  (extremely useful) 
  vimdiff  filename.txt  filename.txt.backup
  when diff window open
  [c  (Go to the next change inside vimdiff)
  ]c  (Go to the previous change inside vimdiff)
  =====================================
  
  Page 124 is Useful
  
  
  
----
  ====================================
  (extremely useful)
  :vimgrep search-pattern   filename.*
  (search for the search pattern inside all files ending  in .txt in the current directory)
  vimgrep by default will jump to the first file that contains a match,
  :cn (will jump to the next file)
  :clist    (view all files match the pattern)
  
  
----
  ========================================
  set vim as default editor as follow
  export EDITOR=vi
  
  view all changes done to a file after opening it 
  :changes
  
  
  
  view ascii code of a charactor
  ga
  
  
  ===================================
  (extremely useful)
  vim -b  binaryfile (edit binary files in vim editor)
  
  
  
----
  ===========================================
  terrible  useful，release  your  mouse：
  paste  content  copy  by  yw  in  command line
  1.  “ayw   copy  the  search  content
  2. Ctrl-R  and  input  a    to paste the content
  detailed introduction  below:
  There are times when you're tempted to lift your hand from the keyboard to the mouse, idly wondering if there's a better way. One such case is taking text from a buffer and placing it into Command-line mode. For example, performing text substitution with %s, or invoking a shell command with :!. Many Vim users will reach for the mouse and use the operating system's copy and paste feature to do this, but there's a quicker way provided by Vim's registers.
  The CTRL-R (:help i_CTRL-R) command can insert the contents of a register in Insert or Replace mode. This is known as a "special key" (:help ins-special-keys). The great thing about this shortcut is you can reuse it to put registers into Command-line mode. For example, let's say you've got some text you want to search for in a buffer. First yank the text into a register, and then paste it with CTRL-R:
  In Normal mode, type "ayw to yank a wordPress escape, and then / to searchThen press CTRL-R and a to put register a
  A shorter way to do this is to use the default register. Typing yw will yank up to the word boundary into the default register, and then typing CTRL-R_" will put it into the command-line. It's worth practicing using this, particularly if you haven't got used to working with registers yet.
  
----
  ====================================
  (extremely useful!!!!!)
  folder code
  za (Toggle the fold under the cursor)
  zR (unfold all folds)
  zm (Fold everything back again)
  :set foldmethod = manual
  
  zf/pattern  (to fold lines selected by the search pattern)
  
  :range fold  (To fold lines specified by a range)
  :mkview (save all your folds as show above)
  
  :loadview
   
----
   ***********************************************************
   
   ************************************************************
   plugin

    ctags
    :ta main  (jump to the definition)
:ta /^get   (jump to the match pattern)
    =====================================
    NERD  Tree  (specially useful)
    =====================================
    autocorrect.vim  (nice)
    =====================================
    (extremely userful!!!)
    Align.vim

    before align 
    a = 1
    hello world = 2
    sh = 3

    after align 
    a                                      =  1
    hello word                      =  2
    sh                                     = 3 

    perform 
    visual  mode select align area and input
    :'<,'>Align = 
    "'
