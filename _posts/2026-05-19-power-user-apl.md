# Power User APL
<sub>2026-05-19</sub>

I'm a power user. Here's how I make Dyalog APL (and other array langs) work for me.

## `~/.XCompose`
1st make symbols work.  
<https://apl.wiki/Typing_glyphs_on_Linux#XCompose_(backtick/prefix/dead_key)>  
<https://mlochbaum.github.io/BQN/editors#xkb-unix>  
<https://github.com/MaxCan-Code/MaxCan-Code/blob/7535c4f9b039c3af16d5d08c0c1f1b02468f8155/symlinks/.XCompose>

## Shell Pipes
Piping seems to work for all langs. Nice for quick experiments in the shell.
```sh
$ echo ⎕se.r⍳3 4\\n]repr ⍳3 4|mapl -b -s
      ⎕se.r⍳3 4
3 4⍴(2⍴1) (1 2) (1 3) (1 4) (2 1) (2⍴2) (2 3) (2 4) (3 1) (3 2) (2⍴3) (3 4)
      ]repr ⍳3 4
(3 4⍴(2⍴1) (1 2) (1 3) (1 4) (2 1) (2⍴2) (2 3) (2 4) (3 1) (3 2) (2⍴3) (3 4))
$ echo ↕3‿4\\n•Repr↕3‿4|bqn
┌─
╵ ⟨ 0 0 ⟩ ⟨ 0 1 ⟩ ⟨ 0 2 ⟩ ⟨ 0 3 ⟩
  ⟨ 1 0 ⟩ ⟨ 1 1 ⟩ ⟨ 1 2 ⟩ ⟨ 1 3 ⟩
  ⟨ 2 0 ⟩ ⟨ 2 1 ⟩ ⟨ 2 2 ⟩ ⟨ 2 3 ⟩
                                  ┘
   "(3‿4⥊⟨0‿0,0‿1,0‿2,0‿3,1‿0,1‿1,1‿2,1‿3,2‿0,2‿1,2‿2,2‿3⟩)"
$ echo '!3 4\n`k(!)3 4'|k
(0 0 0 0 1 1 1 1 2 2 2 2
 0 1 2 3 0 1 2 3 0 1 2 3)
"(0 0 0 0 1 1 1 1 2 2 2 2;0 1 2 3 0 1 2 3 0 1 2 3)"
{% raw %}$ echo "i.3 4\n{{(5!:5)<'y'}}i.3 4\n{{(5!:5)<'y'}}<\"1 i.3 4"|jconsole{% endraw %}
0 1  2  3
4 5  6  7
8 9 10 11
i.3 4
0 1 2 3;4 5 6 7;8 9 10 11
```

## Big Arrays
Avoid flooding my screen.
```sh
$ echo ⎕se.d⍳2/3 4|mapl -b -s>_
$ echo ↕2/3‿4|bqn>_
$ echo "!,/2#'3 4"|k>_
$ echo i.2#3 4|jconsole>_
```
More cumbersome way:
```sh
$ echo "'_'1⊂⍛⎕nput⍨⎕se.d⍳2/3 4\t"|mapl -b -s
$ echo '"_"•FChars•Fmt↕2/3‿4'|bqn
$ echo "(,\"_\")0:,/'\$!,/2#'3 4"|k
$ echo "(<'_')1!:2~,\":i.2#3 4"|jconsole
```
In APL session:
```sh
$ echo "(⍴,≡)_←⍳2/3 4\t⍝ then ⎕ed'_'"|mapl -b -s
      (⍴,≡)_←⍳2/3 4    ⍝ then ⎕ed'_'
3 3 4 4 2
```

## `~/dyalog.files`
Undocumented. See
<https://github.com/Dyalog/qSE/blob/561e2c0f9c151fe280f571079f5c3d276f715939/StartupSession.aplf#L160>
```
$ cat ~/dyalog.files/StartupSession/_/_.apln
:namespace _
    ⎕se.(u←Dyalog.Utils) ⋄ ⎕se.(r←u.repObj) ⋄ ⎕se.(d←1 1 0 1∘u.disp) ⋄ #.⎕pw←¯1+2*15
:endnamespace
```

## Vi-Style Modal Editing
### `~/.inputrc` & `rlwrap`
```sh
$ cat ~/.inputrc
# $include /etc/inputrc
set editing-mode vi
set show-mode-in-prompt on
$if term=linux
        set vi-ins-mode-string \1\e[?0c\2
        set vi-cmd-mode-string \1\e[?8c\2
$else
        set vi-ins-mode-string \1\e[6 q\2
        set vi-cmd-mode-string \1\e[2 q\2
$endif
```
My rlwrap flags:
```sh
$ rlwrap -acrm -D 2 mapl -b -s
```
I used to use these, but global XCompose works better for f/t motions.  
<https://github.com/mlochbaum/BQN/blob/master/editors/inputrc>  
<https://gist.github.com/0racle/bdaeb945cf42de317a48db7b1529f0fe>

### Ride Extension
<https://github.com/Dyalog/ride/blob/8c89ebbadaae55314d3283818cf999fe4a2cd95a/sample-extensions/vim.js>

### APLK
Also undocumented. I dug into it for work. See
<https://docs.dyalog.com/20.0/unix-installation-and-configuration-guide/configuration-parameters/environment-variables#_table-1>

Proof of concept:  
`$ echo ",⍤¯1⊃⊃⎕shell'diff -u \$DYALOG/aplkeys default'|mapl -b -s"`
```diff
-M0=Nrm:
+M0=Ins:    ,    ,, 105
+M3=Nrm:  27
-,UC:		27 91 65	+ Up cursor
-,DC:		27 91 66	+ Down Cursor
-,RC:		27 91 67	+ Right Cursor
-,LC:		27 91 68	+ Left Cursor
+,UC:		27 91 65,,,107	+ Up cursor
+,DC:		27 91 66,,,106	+ Down Cursor
+,RC:		27 91 67,,,108	+ Right Cursor
+,LC:		27 91 68,,,104	+ Left Cursor
-,EP=Esc:	27		+ EscaPe
+,EP=Esc:	,,,27		+ EscaPe
```
