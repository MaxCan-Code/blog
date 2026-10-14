# Tacit in Practice

*(through 4 simple problems)*

<sub>2026-10-15</sub>

Max Sun (views are my own)
Slides: <https://maxsun.best>

# Outline

⍨  APL ∧ Myself
?  Intro demo ⋄ Why (not) Tacit
4️⃣ Simple problems
⎕  Tools ∧ Resources ∧ Questions

------------------------------------------------------------------------

# Disclaimer

Views are my own
Not telling you how to code
Code I write for myself

. . .

Next: ⍨ APL ∧ Myself

------------------------------------------------------------------------

# ⍨ APL ∧ Myself

<https://youtube.com/playlist?list=PLdshoJrUkl-o>

- \'23: Learned APL on the job

- Likes: tools of thought (TLA+, Uiua, bivectors, ...)

- Presented at Toronto, US, Taiwan, (+UK) 🇨🇦 🇺🇸 🇹🇼 🇬🇧

- 1st contact: tacit videos

  - → habit

- Arrays: SQL (ETL, EDA), nested CF

- Taste ∧ Style ← Conor, Aaron, Adám

  - Modern, well-commented

. . .

Next: Intro demo

------------------------------------------------------------------------

# Intro demo

<https://apl.wiki> → Split

``` apl
]Box on -trains=tree
]Left

Y←' split by space'

' ' (≠ ⊆ ⊢)Y

⍋ ⍛ (⊂ ⍛ ⌷)Y
```

. . .

Questions? Next: Why (not) tacit

------------------------------------------------------------------------

# 🐘🚻 Why (not) tacit

<table>
<tbody>
<tr>
<td><p>Why tacit</p>
<ol>
<li><p>Early exposure → habit</p></li>
<li><p><code>(f + g)(x)</code> in math</p></li>
<li><p>Notations as a tool of thought</p></li>
<li><p>Ease of expressing FinnAPL idioms</p></li>
<li><p>Suggests more idioms</p></li>
<li><p>Subordination of detail {⍺ ⍵}</p></li>
<li><p>Economic derived primitives</p></li>
</ol>
<p>Attract bright users/content creators from FP<br />
Works across array langs (J, K, BQN)</p></td>
<td><p>. . .</p>
<p>Why not tacit</p>
<ol>
<li><p>Tradfns most APL life → habit</p></li>
<li><p>Betrays right-to-left eval</p></li>
<li><p>Notations as a tool against thought</p></li>
<li><p>Harder to express FinnAPL idioms</p></li>
<li><p>Doesn’t suggest more idioms</p></li>
<li><p>Adds more syntax detail (f g h)</p></li>
<li><p>Overly economic derived primitives</p></li>
</ol>
<p>Upsets users
Doesn’t work across array langs (J hook vs Dyalog atop)</p>
<p>. . .</p>
<p>(special thanks: ngn, TonyC [apl.farm])</p></td>
</tr>
</tbody>
</table>

. . .

## Many sides of APL:

Biz, enterprise support\
Playful, insightful notation\
Right style for the job

. . .

Questions? Next: \<?\>

------------------------------------------------------------------------

# 4️⃣ simple problems

1.  Make list of strings

        Y←' make list of strings'
        ⊃ ⍛ ≠ ⍛ ⊆ Y

2.  Probe mystery array

        (≡ , ⍴)      mysterY
        X(↑ ⍪ - ⍛ ↑) mysterY

3.  Drop by index

        Y←'so⍛me ex⊇tra cha rs'
        X(⍳∘≢ ⍛ ~⍨ ⊇ ⊢)Y
         (⍳∘≢ , ⍪)     Y

4.  Sort by (column)

        X(⊇⍤1   ⍋ ⍛ ⊇ ⊢)Y
        f    ⍛ (⍋ ⍛ ⊇)  Y

. . .

Next: \<?\>

------------------------------------------------------------------------

# Make list of strings

          ⍝ split segmented string
          Y←' make list of strings'
          ]Repr Split Y
    'make' 'list' 'of' 'strings'

. . .

          ' '(    ≠ ⊆ ⊢)Y     ⍝ apl.wiki

          ' '(⊃ ⍛ ≠ ⊆ ⊢)Y     ⍝ Adám Dyalog '22
             (⊃ ⍛ ≠ ⊆ ⊢)Y

. . .

              ⊃ ⍛ ≠ ⍛ ⊆ Y   ⍝ 👑

. . .

Questions? Next: \<?\>

------------------------------------------------------------------------

# Probe mysterY array

<table>
<tbody>
<tr>
<td><pre class="apl"><code>42⎕atx&#39;mysterY&#39;   ⍝ ⎕nc⊆
⍝ mysterY         ⍝ ❌
⍝ )ed mysterY     ⍝ ❌</code></pre></td>
<td><p>. . .</p>
<pre class="apl"><code>⍝ ⚠️ always assume big∧nested!
DepthShape mysterY
(≡ , ⍴)    mysterY</code></pre></td>
</tr>
<tr>
<td><p>. . .</p>
<pre class="apl"><code>2 FirstLast(≡ , ⍴)¨mysterY</code></pre></td>
<td><p>. . .</p>
<pre class="apl"><code>2 FirstLast mysterY</code></pre></td>
</tr>
<tr>
<td><p>. . .</p>
<pre><code>      2 FirstLast DepthShape¨mysterY
      2 (↑ ⍪ - ⍛ ↑) (≡ , ⍴)     ¨mysterY</code></pre></td>
<td><p>. . .</p>
<pre><code>]Rows on -fold -s=cut
]Repr
⎕se.r←⎕se.Dyalog.Utils.repObj
&#10;⎕se.d←⎕se.Dyalog.Utils.disp
⎕ed&#39;_&#39;⊣_←⎕se.d mysterY
]View</code></pre></td>
</tr>
</tbody>
</table>

. . .

Questions? Next: \<?\>

------------------------------------------------------------------------

# Drop by index

In practice: drop rows from tall array

``` apl
⊢Y←'so⍛me ex⊇tra cha rs'   ⍝ same idea
i j k Deselect Y
```

. . .

``` apl
Y←'so⍛me ex⊇tra cha rs'
⍉ RowNums Y
```

. . .

``` apl
⊢Y←'so⍛me ex⊇tra cha rs'
3 9 17 Deselect Y
```

. . .

<table>
<tbody>
<tr>
<td><pre><code>      3 9 17 Deselect         Y
      3 9 17(⍳∘≢ ⍛ ~⍨ ⊂ ⍛ ⌷ ⊢)Y</code></pre></td>
<td><p>. . .</p>
<pre><code>⍉ RowNums  Y
⍉ (⍳∘≢ , ⍪)Y</code></pre></td>
</tr>
</tbody>
</table>

. . .

Questions? Next: \<?\>

------------------------------------------------------------------------

# Sort by (column)

``` apl
⊢Y←(⍪ , ≢¨) ⊃ ⍛ ≠ ⍛ ⊆' sort by word length'
```

. . .

``` apl
Y←(⍪ , ≢¨) ⊃ ⍛ ≠ ⍛ ⊆' sort by word length'
2 SortByColumn Y
```

. . .

          2 SortByColumn      Y
          2(⌷⍤1 ⍋ ⍛ (⊂ ⍛ ⌷) ⊢)Y

------------------------------------------------------------------------

# Sort by (column)

``` apl
⊣/Y←(⍪ , ≢¨) ⊃ ⍛ ≠ ⍛ ⊆' sort by word length'
Sort←⍛( ⍋ ⍛ (⊂⍛⌷) )       ⍝ Adám Dyalog '22
```

. . .

``` apl
Y←(⍪ , ≢¨) ⊃ ⍛ ≠ ⍛ ⊆' sort by word length'
≢¨Sort ⊣/Y
```

. . .

``` apl
Y←(⍪ , ≢¨) ⊃ ⍛ ≠ ⍛ ⊆' sort by word length'
2∘⌷⍤1 Sort Y
```

. . .

Questions? Next: \<?\>

------------------------------------------------------------------------

# All together

          ]Defs

           Split ← ⊃ ⍛ ≠ ⍛ ⊆

      DepthShape ← ≡ , ⍴
       FirstLast ← ↑ ⍪ - ⍛ ↑

        Deselect ← ⍳∘≢ ⍛ ~⍨ ⊂ ⍛ ⌷ ⊢
         RowNums ← ⍳∘≢ , ⍪

    SortByColumn ← ⌷⍤1   ⍋ ⍛ (⊂ ⍛ ⌷)  ⊢
            Sort ←    ⍛ (⍋ ⍛ (⊂ ⍛ ⌷) )

. . .

                               ┌─ DWIM
                             ⊂⍛⌷
                             └┴── ??

. . .

Questions? Next: \<?\>

------------------------------------------------------------------------

# Digression: Core Language Gap

``` apl
Ⓧ←⊂⍛⌷

Y←'so⍛me ex⊇tra cha rs'

i j k(⍳∘≢⍛~⍨ ⊂⍛⌷ ⊢)Y
i j k(⍳∘≢⍛~⍨   Ⓧ ⊢)Y
```

. . .

          i j k(⍳∘≢⍛~⍨ ⊂⍛⌷ ⊢)Y
          i j k(⍳∘≢⍛~⍨   Ⓧ ⊢)Y
          i j k(⍳∘≢⍛~⍨   ⊇ ⊢)Y   ⍝ `X → ⊇

. . .

                   ⍋ ⍛ (⊂⍛⌷)   Y
                   ⍋ ⍛    ⊇    Y   ⍝   Adám Dyalog '22

          X(⌷⍤1    ⍋ ⍛    ⊇  ⊢)Y
          X(⌷⍤1    ⍋ ⍛ (⊂⍛⌷) ⊢)Y

             ≢¨ ⍛ (⍋ ⍛    ⊇ )  Y
             ≢¨ ⍛ (⍋ ⍛ (⊂⍛⌷))  Y

. . .

<https://apl.wiki/select#cite_ref-4>

. . .

Questions? Next: \<?\>

------------------------------------------------------------------------

# ⎕ Tools ⋄ Resources ⋄ Q∧A

    ]IT

    ]Defs

    ]Box on -trains=tree
    ]Box on -t=tree

. . .

``` apl
]APLcart ⍳∘≢ ~ -l=2
```

1.  <https://apl.wiki/tacit> (on apl.wiki homepage)

    - Translation of \[dfns\] into tacit form
      <https://dfns.dyalog.com/n_tacit.htm>

2.  <https://apl.wiki/train#History>

    - Phrasal Forms, APL89
      <http://jsoftware.com/papers/fork.htm>

Questions? Next: Aaron

------------------------------------------------------------------------

# Extras

. . .

    ⍰←{⍺←⊢ ⋄ (⍺ ⍺⍺ ⍵)⍵⍵ ⍵}    ⍝ left fork?

    X(⍳∘≢⍛~⍨   ⊇ ⊢)Y
    X ⍳∘≢⍛~⍨ ⍰ ⊇   Y

    X(⌷⍤1    ⍋⍛⊇ ⊢)Y
    X ⌷⍤1 ⍰ (⍋⍛⊇)  Y

. . .

    1 ≢¨{⍺ (⍺⍺⍤Ⓧ⍤1 ⍋⍛Ⓧ ⊢) ⍵}Y

     ⍳∘≢ ⍛ ,∘⍪ Y
    (⍳∘≢   , ⍪)Y
