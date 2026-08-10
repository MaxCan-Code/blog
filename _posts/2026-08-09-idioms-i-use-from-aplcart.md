# Idioms I use from APLcart
<sub>2026-08-09</sub>

0 setup stdlib in my head
```sh
$ echo "
⎕pw←125
⎕se.UCMD'aplcart -?'
(⍴,≡)⎕se.Dyalog.Utils.APLcart''
]aplcart ⍴,≡

X←⊂⍛⌷
]aplcart ⊇
s←' Split Yv at occurrences of the first character (removes separators and empty segments)'
((⋄){⍺⊣⍺.⎕cy⍵}'dfns').disp 2(⌷⍤1⍋⍛X⊢) ⎕← 2(↑⍪-⍛↑) ¯5↓ 2 4 5 6(~⍨∘⍳∘≢X⊢) ⍳∘≢⍛,∘⍪  ≠∘⊃⍨⍛⊆ s
⊃⍪/' '⍪¨⎕se.Dyalog.Utils.APLcart¨'≠ ⊆' '⍳∘≢⍛,' '~⍨∘⍳' '↑⍪-⍛↑' '⎕←' '⌷⍤ ⍋' '.⎕cy' '⍪¨' '⍪/'
]aplcart seg at first char

'_.csv'⎕csv⎕opt'IfExists' 'Replace'⍨ '⍳' 'desc'⍪ ⍳∘≢⍛,∘⍪ ⊃∘⎕nget∘(⊂,1⍨) '_'⊣ '_'1⊂⍛⎕nput⍨ ≠∘⊃⍨⍛⊆ s
⎕csv∘(⊂,⍬ 4 1⍨)'_.csv'
]repr '⍳' 'desc'⍪ ⍳∘≢⍛,∘⍪ ≠∘⊃⍨⍛⊆ s -f=csv -o=_.csv
]get ./_.csv
_
⊃⍪/⎕se.Dyalog.Utils.APLcart¨'⍛ ⎕nput' '⊂,1'
]aplcart csv -l
"|mapl -b -s

      ⎕pw←125
      ⎕se.UCMD'aplcart -?'
───────────────────────────────────────────────────────────────────────────────

]TOOLS.APLCart

Access a searchable collection of over 3000 short APL phrases

    ]APLCart [<terms>] [-list[=n]] [-url] [-browser] [-popup] [-theme=b|w] [-refresh]

]APLCart -??  ⍝ for details and examples

]APLCart is a frontend for the ⎕SE.Dyalog.Utils.APLcart function.

      (⍴,≡)⎕se.Dyalog.Utils.APLcart''
3776 2 2
      ]aplcart ⍴,≡
X,Y,Z:any M,N:num I,J:int A,B:Bool C,D:char f,g,h:fn ax:axis s:scal v:vec m:mat
───────────────────────────────────────────────────────────────────────────────
───────────────────────────────────────────────────────────────────────────────
Showing 0 of 0 matches (suggestions? mailto://ideas@aplcart.info )

      X←⊂⍛⌷
      ]aplcart ⊇
X,Y,Z:any M,N:num I,J:int A,B:Bool C,D:char f,g,h:fn ax:axis s:scal v:vec m:mat
─────────────────────────────────────────────────────────────────────────────────────
Iv⊂⍛⌷Y         ⍝ Select major cells Iv from Y
Iv⊂⍛⌷Y         ⍝ Permute: Reorder major cells of Y according to permutation vector Iv
Im(⌷⍤¯1 99)Y   ⍝ Select: each major cell of Im selects a cell from Y
Iv(⊃⍛⌷⍤0 99)Y  ⍝ Select: each element of Iv selects a cell from Y
Xv(∧/∊⍨)Yv     ⍝ Is Xv a Superset of Yv?
─────────────────────────────────────────────────────────────────────────────────────
Showing 5 of 5 matches
      s←' Split Yv at occurrences of the first character (removes separators and empty segments)'
      ((⋄){⍺⊣⍺.⎕cy⍵}'dfns').disp 2(⌷⍤1⍋⍛X⊢) ⎕← 2(↑⍪-⍛↑) ¯5↓ 2 4 5 6(~⍨∘⍳∘≢X⊢) ⍳∘≢⍛,∘⍪  ≠∘⊃⍨⍛⊆ s
1  Split
3  at
7  first
8  character
┌─┬─────────┐
│1│Split    │
├─┼─────────┤
│3│at       │
├─┼─────────┤
│8│character│
├─┼─────────┤
│7│first    │
└─┴─────────┘
      ⊃⍪/' '⍪¨⎕se.Dyalog.Utils.APLcart¨'≠ ⊆' '⍳∘≢⍛,' '~⍨∘⍳' '↑⍪-⍛↑' '⎕←' '⌷⍤ ⍋' '.⎕cy' '⍪¨' '⍪/'

 Xs(≠⊆⊢)Yv                 Split Yv at occurrences of Xs (removes separators and empty segments)
 (~∧≠\)⍤=∘''''⍛⊆Dv         Extract text (without quotes) in expression
 {0⎕JSON¨⍵⊆⍨⍵≠⎕UCS 10}Dv   Convert JSON Lines text Dv to APL vector
 Av{≠\⍵\⍺≠¯1↓0,⍺}Bv        Compression vector Av for partitioned array indicated by Bv (Fast Av/⍨≢¨⊆⍨Bv)

 ⍳∘≢⍛,Ym                   Attach row numbers to a matrix

 I(⊂⍤~⍨∘⍳∘≢⌷⊢)Y            Major cells of Y except those enumerated in I

 Iv(↑⍪-⍛↑)Y                Take first and last Iv items along leading axes of Y

 ⎕←x                       Output x to the session via stdout (with trailing line break)

 (⊂⍤⍋⍛⌷⍤1)Y                Sort each row in ascending order
 (⊂⍤⍋⍛⌷⍤¯1)Y               Sort major cells ascending
 Is(⌷⍤1⊂⍤⍋⍛⌷⊢)Y            Sort Y ascending according to column Is
 ((⍉⊂⍤⍋⍛⌷⍤1∘⍉)⍤2)Y         Sort each column in ascending order

 {(⍎⍵⎕NS⍬).⎕CY ⍵}Dv        Import workspace Dv into a namespace so an item can be called using wsname.name
 {(⍎⍵⎕NS⍬).⎕CY ⍵}'dfns'    Import dfns workspace into a namespace called dfns so dfn can be called using dfns.name
 ({⍵⊣⍵.⎕CY'dfns'}()).name  Call function “name” from the dfns workspace without polluting the current workspace


 ⍪/Yv                      Fast: The enclose of the items of Yv (which must be of depth 2) catenated along their first axes
 Xv{⊃⍪/1↓,⍺⊂⍛,⍪⍵}Yv        Join vector of vectors Yv using separator Xv
 {(⊂⍋∊⍳∘≢¨⍵)⌷⊃⍪/⍵}Yv       Mesh major cells of elements of Yv
      ]aplcart seg at first char
X,Y,Z:any M,N:num I,J:int A,B:Bool C,D:char f,g,h:fn ax:axis s:scal v:vec m:mat
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
(⊃+.=⊢)Dv                                                            ⍝ Number of segments in delimited string Dv where the
                                                                     first character is the delimiter ≢ ⍴
(¯1+¯2-/∘⍸⊃⍛=,1⍨)Dv                                                  ⍝ Segment lengths (excluding delimiters) in delimited
                                                                     string Dv where the first character is the delimiter
Av{⍵/⍨(+\⍵=⊃⍵)∊⍸⍺}Dv                                                 ⍝ Compress delimited string Dv (where the first
                                                                     character is the delimiter) using compression vector Av
{⍺←⊃⌽⍵ ⋄ 1↓¨⍺(=⊂⊢)⍵}Dv                                               ⍝ Vector of character vectors constructed from the
                                                                     character vector Dv where the first character is the
                                                                     delimiter
Is{r←+\⍵=d←⊃⍵ ⋄ 0<⍺:⍵/⍨r>⍺ ⋄ ⍵/⍨r≤⍺+⊃⌽r}Dv                           ⍝ Drop first Is (if negative: last |Is) segments from
                                                                     delimited string Dv where the first character is the
                                                                     delimiter
Is{s←⊃⌽r←+\⍵=d←⊃⍵ ⋄ 0<⍺:(⍵/⍨r≤⍺),d⍴⍨0⌈⍺-s ⋄ (d⍴⍨0⌈-⍺+s),⍵/⍨r>⍺+s}Dv  ⍝ Take first Is (if negative: last |Is) segments from
                                                                     delimited string Dv where the first character is the
                                                                     delimiter
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
Showing 6 of 6 matches

      '_.csv'⎕csv⎕opt'IfExists' 'Replace'⍨ '⍳' 'desc'⍪ ⍳∘≢⍛,∘⍪ ⊃∘⎕nget∘(⊂,1⍨) '_'⊣ '_'1⊂⍛⎕nput⍨ ≠∘⊃⍨⍛⊆ s
      ⎕csv∘(⊂,⍬ 4 1⍨)'_.csv'
  1  Split          ⍳  desc
  2  Yv
  3  at
  4  occurrences
  5  of
  6  the
  7  first
  8  character
  9  (removes
 10  separators
 11  and
 12  empty
 13  segments)
      ]repr '⍳' 'desc'⍪ ⍳∘≢⍛,∘⍪ ≠∘⊃⍨⍛⊆ s -f=csv -o=_.csv
      ]get ./_.csv
#._
      _
 ⍳  desc
 1  Split
 2  Yv
 3  at
 4  occurrences
 5  of
 6  the
 7  first
 8  character
 9  (removes
10  separators
11  and
12  empty
13  segments)
      ⊃⍪/⎕se.Dyalog.Utils.APLcart¨'⍛ ⎕nput' '⊂,1'
 Cv⊂⍛⎕NPUT Dv              Write text (vector or matrix or vector of vectors) Cv to Unicode file Dv
 Xs(⎕FIX⊢⊣⊂∘⎕SRC⍛⎕NPUT)Dv  Save scripted object Xs (ref) to synced file Dv
 (⊃∘⎕NGET⊂,1⍨)Dv           Read Unicode text file Dv content as nested vector
      ]aplcart csv -l
X,Y,Z:any M,N:num I,J:int A,B:Bool C,D:char f,g,h:fn ax:axis s:scal v:vec m:mat
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
r←⎕CSV data                           ⍝ Convert CSV data to APL matrix
r←data {header} ⎕CSV format_spec      ⍝ Convert CSV data from APL matrix
r←(⎕CSV⍠1)data                        ⍝ Convert CSV data to APL inverted table (character data as matrices)
r←(⎕CSV⍠2)data                        ⍝ Convert CSV data to APL inverted table (character data as vectors of vectors)
r←data {header}(⎕CSV⍠1)format_spec    ⍝ Convert CSV data from APL inverted table (character data as matrices)
r←data {header}(⎕CSV⍠2)format_spec    ⍝ Convert CSV data from APL inverted table (character data as vectors of vectors)
{⎕CSV ⍵ ⍬ 4 1}Dv                      ⍝ Data matrix and column titles as 2-element vector from CSV (file or vector of
                                      vectors), with apparent numbers as numbers
{,⎕CSV ⍵ ⍬ 2}Dv                       ⍝ Numeric vector from text file with one number on each line
]EXPERIMENTAL.Get                     ⍝ Fetch data/code in many formats from local or remote sources
]OUTPUT.Repr                          ⍝ Represent given value as APL/APLAN/JS/JSON/XML/CSV/SSV/PSV/TSV
⎕DMX.(Category ENX)≡'Native files'60  ⍝ Invalid CSV source in right argument
⎕DMX.(Category ENX)≡'Native files'61  ⍝ Invalid CSV source type in right argument
⎕DMX.(Category ENX)≡'Native files'64  ⍝ Invalid CSV destination in right argument
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
Showing 13 of 13 matches (-list=<n> to show no more than <n>)
```
