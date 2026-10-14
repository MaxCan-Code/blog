# Tacit in Practice
<sub>*through 4 simple problems*</sub>  
<sub>2026-10-15</sub>  
<sub>updated 2026-11-01</sub>  
<https://dyalog.com/user-meetings/dyalog26.htm>

Max Sun (views are my own)  
Slides: <https://maxsun.best>

# Outline
<pre>
⍨  APL ∧ Myself
?  Intro demo ⋄ Why (not) Tacit
4&#65039;&#8419; Simple problems
⎕  Tools ∧ Resources ∧ Questions
</pre>
---
# Disclaimer
Views are my own  
Not telling you how to code  
Code I write for myself

---
# ⍨ APL ∧ Myself
<https://youtube.com/playlist?list=PLdshoJrUkl-o>
- \'23: Learned APL on the job
- Likes: tools of thought (TLA+, Uiua, bivectors, ...)
- Presented at Toronto, US, Taiwan, (+UK) &#127464;&#127462; &#127482;&#127480; &#127481;&#127484; &#127468;&#127463;
- 1st contact: tacit videos
  - → habit
- Arrays: SQL Tables, CSVs, nested CF
- Taste ∧ Style ← Conor, Aaron, Adám
  - Modern, well-commented

---
# Intro demo
<https://apl.wiki> → Split
```apl
      Y←' split by space'
       ' ' (≠    ⊆      ⊢) Y
┌─────┬──┬─────┐
│split│by│space│
└─────┴──┴─────┘
      (' '  ≠ Y) ⊆ (' ' ⊢  Y)
┌─────┬──┬─────┐
│split│by│space│
└─────┴──┴─────┘
       ' ' (≠    ⊆      ⊢) Y
            ↓           ↓
      (' '    Y)   (' '    Y)
                 ↓
      (' '  ≠ Y) ⊆ (' ' ⊢  Y)


         ⍺ (f    g      h) ⍵     ⍝ substitute
            ↓           ↓
      (  ⍺    ⍵)   (  ⍺    ⍵)
                 ↓
      (  ⍺  f ⍵) g (  ⍺ h  ⍵)


           (f    g      h) ⍵     ⍝ 1-sided
            ↓           ↓
      (       ⍵)   (       ⍵)
                 ↓
      (     f ⍵) g (    h  ⍵)    ⍝ (f + h)(x) ←→ f(x) + h(x)


         ⍺ (     g      h) ⍵     ⍝ no f
                        ↓
                   (  ⍺    ⍵)
                 ↓
                 g (  ⍺ h  ⍵)


           (     g      h) ⍵
                        ↓
                   (       ⍵)
                 ↓
                 g (    h  ⍵)
```
```apl
      3 1 2 ⊂     ⍛  ⌷ Y
p s
           (⊂ 3 1 2) ⌷ Y
p s
          ┌──────↘︎
      3 1 2 ⊂     ⍛  ⌷ Y
           (⊂ 3 1 2) ⌷ Y
          ┌──────↘︎
          ⍺ f     ⍛  g ⍵
           (f     ⍺) g ⍵      ⍝ substitute

            f     ⍛  g ⍵      ⍝ 1-sided
           (f     ⍵) g ⍵
                  ↑

       ⍋ ⍛  (⊂    ⍛   ⌷) Y
   abceilppssty
       ⍋ ⍛  (⊂    ⍛   ⌷) Y
      (⍋ Y) (⊂    ⍛   ⌷) Y
         ↑
            (⊂ (⍋ Y) )⌷  Y
                  ↑
   abceilppssty

```

---

# 🐘🚻 Why (not) tacit

| Why tacit                                     | Why not tacit                                           |
| ---                                           | ---                                                     |
| Early exposure → habit                        | Tradfns most APL life → habit                           |
| `(f + g)(x)` in math                          | Betrays right-to-left eval                              |
| Notations as a tool of thought                | Notations as a tool against thought                     |
| Ease of expressing FinnAPL idioms             | Harder to express FinnAPL idioms                        |
| Suggests more idioms                          | Doesn\'t suggest more idioms                            |
| Subordination of detail `{⍺ ⍵}`               | Adds more syntax detail `(f g h)`                       |
| Economic derived primitives                   | Overly economic derived primitives                      |
| Attract bright users/content creators from FP | Upsets users                                            |
| Works across array langs (J, K, BQN)          | Doesn't work across array langs (J hook vs Dyalog atop) |
|                                               | (special thanks: ngn, TonyC [<https://apl.farm>])                 |

## APL has many sides

Biz, enterprise support  
Playful, insightful notation  
Right style for the job

## Where tacit works
Short idioms (<7 trains) <https://aplcart.info?q=/\((?:[^\s()]*?[^\w\s\()]){6,7}[^\s()]*\)/>  
Formulas: <https://aplcart.info?q=/deviation|variance|correlation/>

---

# 4&#65039;&#8419; simple problems

1. Make list of strings
   ```apl
   Y←' make list of strings'
   ⊃ ⍛ ≠ ⍛ ⊆ Y
   ```
1. Probe mysterY array
   ```apl
    (≡ ,     ⍴) mysterY
   X(↑ ⍪ - ⍛ ↑) mysterY
   ```
1. Drop by index
   ```apl
   Y←'so⍛me ex⊇tra cha rs'
   X(⍳∘≢ ⍛ ~⍨ ⊇ ⊢) Y
    (⍳∘≢      , ⍪) Y
   ```
1. Sort by (column)
   ```apl
     X(⊇⍤1  ⍋ ⍛ ⊇ ⊢) Y
     f   ⍛ (⍋ ⍛ ⊇)   Y
   ⍋∘f        ⍛ ⊇    Y
   ```

---

# Make list of strings
```apl
      ⍝ split segmented string
      Y←' make list of strings'
      ]Repr Split Y
'make' 'list' 'of' 'strings'
```
<pre>
      ' '(    ≠   ⊆ ⊢)Y    ⍝ apl.wiki

      ' '(⊃ ⍛ ≠   ⊆ ⊢)Y    ⍝ Adám Dyalog '22
         (⊃ ⍛ ≠   ⊆ ⊢)Y
          ⊃ ⍛ ≠ ⍛ ⊆   Y    ⍝ &#128081;
</pre>
---
# Probe mysterY array
<pre>
      mysterY←⎕csv'mysterY.csv'
      42⎕atx'mysterY'   ⍝ ⎕nc⊆
2.1
      ⍝ mysterY         ⍝ &#10060;
      ⍝ )ed mysterY     ⍝ &#10060;
</pre>
<pre>
      ⍝ &#9888;&#65039; always assume big∧nested!
      DepthShape mysterY
2 7 9
      (≡ , ⍴)    mysterY
2 7 9
      ⍝ depth 2. scary
</pre>
```apl
      2 FirstLast (≡ , ⍴) ¨ mysterY
 1 1  1 2  1 2  1 2  1 2  1 2  1 2  1 2  1 2
 1 1  1 2  1 2  1 2  1 2  1 2  1 2  1 2  1 2
 1 1  1 2  1 2  1 2  1 2  1 2  1 2  1 2  1 2
 1 1  1 2  1 2  1 2  1 2  1 2  1 2  1 2  1 2
      ⍝ depth 1 & small shape. safe to print
```
```apl
      2 FirstLast mysterY
 6  AA  AB  AC  AD  AE  AF  AG  AH
 6  BA  BB  BC  BD  BE  BF  BG  BH
 6  FA  FB  FC  FD  FE  FF  FG  FH
 6  GA  GB  GC  GD  GE  GF  GG  GH
```
```apl
      2 FirstLast   DepthShape ¨ mysterY
      2 (↑ ⍪ - ⍛ ↑) (≡ , ⍴)    ¨ mysterY
```
```apl
      ⍝ honourable mentions
      ]Rows on -fold -style=cut -fns=on
Was OFF -style=long -fold=off -fns=off

      4/4⌿mysterY
 6  6  6  6  AA  AA  AA  AA  AB  AB  AB  AB  AC  AC  AC  AC  AD  AD  AD  AD ···
 6  6  6  6  AA  AA  AA  AA  AB  AB  AB  AB  AC  AC  AC  AC  AD  AD  AD  AD ···
 6  6  6  6  AA  AA  AA  AA  AB  AB  AB  AB  AC  AC  AC  AC  AD  AD  AD  AD ···
 6  6  6  6  AA  AA  AA  AA  AB  AB  AB  AB  AC  AC  AC  AC  AD  AD  AD  AD ···
 6  6  6  6  BA  BA  BA  BA  BB  BB  BB  BB  BC  BC  BC  BC  BD  BD  BD  BD ···
 6  6  6  6  BA  BA  BA  BA  BB  BB  BB  BB  BC  BC  BC  BC  BD  BD  BD  BD ···
 6  6  6  6  BA  BA  BA  BA  BB  BB  BB  BB  BC  BC  BC  BC  BD  BD  BD  BD ···
 6  6  6  6  BA  BA  BA  BA  BB  BB  BB  BB  BC  BC  BC  BC  BD  BD  BD  BD ···
 6  6  6  6  CA  CA  CA  CA  CB  CB  CB  CB  CC  CC  CC  CC  CD  CD  CD  CD ···
 6  6  6  6  CA  CA  CA  CA  CB  CB  CB  CB  CC  CC  CC  CC  CD  CD  CD  CD ···
 6  6  6  6  CA  CA  CA  CA  CB  CB  CB  CB  CC  CC  CC  CC  CD  CD  CD  CD ···
 6  6  6  6  CA  CA  CA  CA  CB  CB  CB  CB  CC  CC  CC  CC  CD  CD  CD  CD ···
 6  6  6  6  DA  DA  DA  DA  DB  DB  DB  DB  DC  DC  DC  DC  DD  DD  DD  DD ···
 6  6  6  6  DA  DA  DA  DA  DB  DB  DB  DB  DC  DC  DC  DC  DD  DD  DD  DD ···
 6  6  6  6  DA  DA  DA  DA  DB  DB  DB  DB  DC  DC  DC  DC  DD  DD  DD  DD ···
 6  6  6  6  DA  DA  DA  DA  DB  DB  DB  DB  DC  DC  DC  DC  DD  DD  DD  DD ···
 6  6  6  6  EA  EA  EA  EA  EB  EB  EB  EB  EC  EC  EC  EC  ED  ED  ED  ED ···
···············································································
 6  6  6  6  GA  GA  GA  GA  GB  GB  GB  GB  GC  GC  GC  GC  GD  GD  GD  GD ···
 6  6  6  6  GA  GA  GA  GA  GB  GB  GB  GB  GC  GC  GC  GC  GD  GD  GD  GD ···
 6  6  6  6  GA  GA  GA  GA  GB  GB  GB  GB  GC  GC  GC  GC  GD  GD  GD  GD ···
```
```apl
      ]Repr ⊃mysterY
(,'6')
      ⎕se.r←⎕se.Dyalog.Utils.repObj
      ⎕se.r ⊃mysterY
,'6'
```
```apl
      ⎕se.d←⎕se.Dyalog.Utils.disp
      ⎕ed'_'⊣_←⎕se.d mysterY
      ]View
```
---
# Drop by index
```apl
      ⍝ in practice: drop rows from tall array
      ⊢Y←'so⍛me ex⊇tra cha rs'    ⍝ same idea
so⍛me ex⊇tra cha rs
      i j k Deselect Y
some extra chars
```
```apl
      ⍉ RowNums Y
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
s o ⍛ m e   e x ⊇  t  r  a     c  h  a     r  s
      3 9 17 Deselect Y
some extra chars
```
```apl
      3 9 17 Deselect         Y
      3 9 17(⍳∘≢ ⍛ ~⍨ ⊂ ⍛ ⌷ ⊢)Y
```
```apl
      ⍉ RowNums          Y
      ⍉    (⍳∘≢    ,  ⍪) Y
      ⍉ ⍪ ∘ ⍳∘≢ ⍛  ,     Y
      ⍉     ⍳∘≢ ⍛ (,⍤¯1) Y
```
---
# Sort by (column)
```apl
      ⊢Y←(⍪ , ≢¨) ⊃ ⍛ ≠ ⍛ ⊆' sort by word length'
┌──────┬─┐
│sort  │4│
├──────┼─┤
│by    │2│
├──────┼─┤
│word  │4│
├──────┼─┤
│length│6│
└──────┴─┘
      2 SortByColumn Y
┌──────┬─┐
│by    │2│
├──────┼─┤
│sort  │4│
├──────┼─┤
│word  │4│
├──────┼─┤
│length│6│
└──────┴─┘
```
```apl
      2 SortByColumn        Y
      2 (⌷⍤1 ⍋ ⍛ (⊂ ⍛ ⌷) ⊢) Y
```
```apl
      ⊣/Y
┌────┬──┬────┬──────┐
│sort│by│word│length│
└────┴──┴────┴──────┘
      ≢¨ ⍛ Sort ⊣/Y
┌──┬────┬────┬──────┐
│by│sort│word│length│
└──┴────┴────┴──────┘
```
```apl
      ⍝ different from the talk. slight improvement
      Sort←⍋ ⍛ (⊂ ⍛ ⌷)    ⍝ Adám Dyalog '22
      2 (⌷⍤1   Sort ⊢) Y
      2∘ ⌷⍤1 ⍛ Sort    Y
```
---
# All together
```
          ]Defs

           Split ← ⊃ ⍛ ≠ ⍛ ⊆

      DepthShape ← ≡ , ⍴
       FirstLast ← ↑ ⍪ - ⍛ ↑

        Deselect ← ⍳∘≢ ⍛ ~⍨ ⊂ ⍛ ⌷  ⊢
         RowNums ← ⍳∘≢ ⍛ , ∘ ⍪

    SortByColumn ← ⌷⍤1 ⍋ ⍛ (⊂ ⍛ ⌷) ⊢
            Sort ←     ⍋ ⍛ (⊂ ⍛ ⌷)

                                ┌─ DWIM
                            ⊂ ⍛ ⌷
                            └─┴── ?? suggests nothing
                                     detail to subordinate
```
---
# Digression: Core Language Gap
```apl
      Ⓧ←⊂⍛⌷
      Y←'so⍛me ex⊇tra cha rs'
      i j k (⍳∘≢ ⍛ ~⍨ Ⓧ ⊢) Y
some extra chars
```
```apl
      i j k (⍳∘≢ ⍛ ~⍨ ⊂⍛⌷  ⊢) Y
      i j k (⍳∘≢ ⍛ ~⍨   Ⓧ  ⊢) Y
      i j k (⍳∘≢ ⍛ ~⍨   ⊇  ⊢) Y    ⍝ `X → ⊇

          X (⌷⍤1 ⍋ ⍛ (⊂⍛⌷) ⊢) Y
          X (⌷⍤1 ⍋ ⍛    ⊇  ⊢) Y

                 ⍋ ⍛ (⊂⍛⌷)    Y
                 ⍋ ⍛    ⊇     Y    ⍝ Adám Dyalog '22

            ≢¨⍛ (⍋ ⍛ (⊂⍛⌷))   Y
            ≢¨⍛ (⍋ ⍛    ⊇ )   Y

                 ⍋∘f  (⍛⊇)    Y    ⍝ another digression
```
<https://apl.wiki/select#cite_ref-4>

---
# ⎕ Tools ⋄ Resources ⋄ Q∧A
``` sh
cat<<EOF|mapl -b -s
]APLcart -url

⎕se.UCMD'Right -?'

]APLcart ]Defs
]APLcart ]Box

]APLcart -list=2 ⍳∘≢ ~
]APLcart -url    ⍳∘≢ ~
EOF
      ]APLcart -url
https://aplcart.info

      ]Right -?
───────────────────────────────────────────────────────────────────────────────

]IT.Right

Open Right Argument window for inline tracing
    ]Right         ⍝ view/edit Inline Tracing Right
    ]Right -aplan  ⍝ ditto, but using array notation


      ]APLcart ]Defs
X,Y,Z:any M,N:num I,J:int A,B:Bool C,D:char f,g,h:fn ax:axis s:scal v:vec m:mat
────────────────────────────────────────────────────────────────────────────────────────────────────
defns←{names←0 {list←0 {space←⎕THIS}}} dfns.defs namelist  ⍝ Extended ]defs
]FN.Defs                                                   ⍝ List single-line dfns, dops, derived
                                                           functions and trains
────────────────────────────────────────────────────────────────────────────────────────────────────
Showing 2 of 2 matches
      ]APLcart ]Box
X,Y,Z:any M,N:num I,J:int A,B:Bool C,D:char f,g,h:fn ax:axis s:scal v:vec m:mat
────────────────────────────────────────────────────────────────────────────────────────────────────
{2⎕NQ⎕SE'FileRead'⊣⎕SE⎕WS'File'⍵}     ⍝ Load Session configuration (including ]box and ]rows
                                      settings) from file Dv
{2⎕NQ⎕SE'FileWrite'⊣⎕SE⎕WS'File'⍵}Dv  ⍝ Save Session configuration (including ]box and ]rows
                                      settings) as file Dv
]OUTPUT.Box                           ⍝ Display output with borders indicating shape, type and
                                      structure
]OUTPUT.Boxing                        ⍝ Display output with borders indicating shape, type and
                                      structure
2⎕NQ⎕SE'FileWrite'                    ⍝ Save Session configuration (including ]box and ]rows
                                      settings) to default session file
────────────────────────────────────────────────────────────────────────────────────────────────────
Showing 5 of 5 matches

      ]APLcart -list=2 ⍳∘≢ ~
X,Y,Z:any M,N:num I,J:int A,B:Bool C,D:char f,g,h:fn ax:axis s:scal v:vec m:mat
───────────────────────────────────────────────────────────────────────────────
I(⊂⍤~⍨∘⍳∘≢⌷⊢)Y       ⍝ Major cells of Y except those enumerated in I
(~0∊×∘|≤∘.<⍨∘⍳∘≢)Bm  ⍝ Is Bm an upper triangular matrix without diagonal?
───────────────────────────────────────────────────────────────────────────────
Showing 2 of 5 matches
      ]APLcart -url    ⍳∘≢ ~
https://aplcart.info?q=⍳∘≢ ~
```
1. apl.wiki → <https://apl.wiki/tacit>
   - Translation of [dfns] into tacit form  
     <https://dfns.dyalog.com/n_tacit.htm>
1. apl.wiki/tacit → <https://apl.wiki/train#History>
   - Phrasal Forms, APL89  
     <http://jsoftware.com/papers/fork.htm>

---
# Extras
```apl
X(⍳∘≢⍛~⍨      ⊇ ⊢)Y
X ⍳∘≢⍛~⍨ ⍰    ⊇   Y

X(⌷⍤1       ⍋⍛⊇ ⊢)Y
X ⌷⍤1    ⍰ (⍋⍛⊇)  Y

⍰←{⍺←⊢ ⋄ (⍺ ⍺⍺ ⍵)⍵⍵ ⍵}    ⍝ left fork?

mysterY←6⍪⍤1⊂⍤1⊢⎕a(⊂⍛⌷)⍨7(⍪⍤0⍤¯1 1)⍥⍳8
```

## \"Youngness\" computations by popular (?) demand
```apl
      ]Output on
      ⍳⍤≢⍛,apl_year    ⍝ estimate. corrections welcome
[
  1 'The Road Ahead'                                               'Morten'    ¯1
  2 'Slowly Getting Faster'                                        'Asher'     22
  3 'Improving APL Threads'                                        'Peter'     21
  4 'Dyalog and AI'                                                'Stefan'    15
  5 'Inside Dyalog Labs – From Prototype to Project'               'Martina'   24
  6 '"Cooler Than Keanu"'                                          'JD'        ¯1
  7 'Web Services Overview'                                        'Brian'     ¯1
  8 'Making Web Services More Accessible'                          'Holden'    18
  9 'Time''s Up'                                                   'RS'        ¯1
 10 'Dyalog Static Analysis Tool – In Practice and the Future'     'Brandon'   21
 11 'Behind the Curtain: The Creation of a New Operator'           'Silas'     22
 12 'EWC in 2026'                                                  'Aarush'    23
 13 'Ten Years Without Workspaces'                                 'Adám'      ¯1
 14 'APL Media Update 2026'                                        'RP'        18
 15 'Co-dfns Update (v6)'                                          'Aaron'     12
 16 'One Extension and Seven New Primitives'                       'Adám'      ¯1
 17 'Testing the Untestable – GUIs, Fuzzers, and Dyalog APL'       'Aarush'    23
 18 'Plots and Tables: A Modern Approach'                          'Jesús'     23
 19 'Think in Arrays: Design, Iterate, and Build in the Age of AI' 'Dave'      ¯1
 20 'Dyalog in the Global Investment Management Architecture'      'Oliver'    ¯1
 21 'Coming Up for Air: What I''d Like to See from Dyalog'         'Gilgamesh' ¯1
 22 'Why CI is (Also) Important in the Age of D-AI-alog'           'Lars'      ¯1
 23 'The APL Forge (Winner) – APLearn, Machine Learning in APL'    'Borna'     24
 24 'The APL Forge (Winner) – Forging Voxels with Dyalog APL'      'Kyle'      25
 25 'The APL Trust – An Update'                                    'Diane'     ¯1
 26 'The Next APL Font Family'                                     'Madeline'  23
 27 'Trying to Make a Point: APL Glyphs in Action'                 'Katya'     26
 28 'Claude is the New Quad'                                       'Mark'      ¯1
 29 'Claude is the New Quad'                                       'RP'        18
 30 'The Newcomer''s Experience: Creating a Video Game in APL'     'Mikaela'   26
 31 'Tacit in Practice'                                            'Max'       23
]
      (⊢⌿,⍥(+⌿)(≠⊣⌿))⍉23≤@3⍤1⊢apl_year    ⍝ presentations / total
10 30
      (+⌿,≢)⊢/∪0 1↓23≤@3⍤1⊢apl_year       ⍝ speakers      / total
9 28
```
[previously (DYNA26)](../../../2026/05/03/dyna26-trip-report.html#youngness-computations)
