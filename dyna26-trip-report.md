# DYNA26 Trip Report
<sub>2026-05-03</sub>

2026 marks 60 years of APL.[^60]

[^60]: 10 + <https://dyalog.com/50-years-of-apl.htm>

DYNA26 lives up to this milestone. Good variety of presentations
and half from young APLers.
The talks themselves will be uploaded so I won't say much on those.
Slides at <https://dyalog.com/north-american-user-meetings/dyna26.htm>

## Day Before: Anime bookstore and Diamond District
I arrived the day before and found Kinokuniya a block from the venue[^knky].
Their Bang Dream and Project Sekai CDs stood out to me. Don't see those often.
They also have Fate/Stay Night and a Touhou data book.
Markup is high but better than nothing.

[^knky]: <https://usa.kinokuniya.com/stores-kinokuniya-new-york>

Next I went to a street of jewellers' shops in the Diamond District,
many of which are customers of BIG.
Mark Wolfson talked about helping family shops with inventory last Sep[^dynaf25].

[^dynaf25]: <https://dyalog.com/north-american-user-meetings/dynafall2025.htm>

## Day of: Dave Thomas, Jacob, and more Bookstore
I got to talk to Dave Thomas[^Dave].
We had more chats in the next few days.

[^Dave]: <https://davethomas.net>

Jacob of FIXAPL[^FIXAPL] joined during Kyle's talk.
The 3 of us went to Kinokuniya.
Search "kinokuniya" in APL Farm[^APL_Farm] for a photo.

[^FIXAPL]: <https://apl.wiki/FIXAPL>
[^APL_Farm]: <https://apl.wiki/APL_Farm>

## Bonus: NixOS NYC Meetup
Shortly after DYNA26 I went to the New York Nix Meetup at Anterior[^nix].
I met the devs behind dune2nix.
We talked about reproducibility problems with Dune and
their S-expressions parser in Nix[^sexp].

[^nix]: <https://meetup.com/new-york-nix-users-group/events/313149220>  
    Also see <https://nixos.org/community> and <https://nix.ug>

[^sexp]: <https://github.com/anteriorcore/dune2nix/blob/master/nix/sexp.nix>  
    Tests included!

I met Jesse[^Jesse] again. We exchanged Nix tricks,
dotfiles management practices, and terminal workflows. Lots to try on my end.

[^Jesse]: <https://psychollama.io>

I met Ben at Anterior, who went to the New York APL Meetup in 2022[^APL22]!
We were both fans of Conor's work and talked about learning from his videos[^Conor].

[^APL22]: <https://twitter.com/code_report/status/1567707315200983040>
[^Conor]: <https://conorshakory.com>

As usual I showcased [tryapl.org](https://tryapl.org) to folks there.
For Evan[^Evan], a seasoned Haskeller,
I brought up the Combinator Graphic[^graphic] for comparison with array langs.
I forgot to bring up [arraybox.dev](https://arraybox.dev) `:(` . Next time I shall.

[^Evan]: <https://evanpiro.com>
[^graphic]: <https://combinatorylogic.com/graphic.html>

### Appendix
DYNA24, NY Nix Meetup, (and LispNYC Social) also fell on the day 2 years ago[^Apr11].
That's where I first met Jesse.

[^Apr11]: <https://dyalog.com/north-american-user-meetings/dyna24.htm>  
    <https://meetup.com/new-york-nix-users-group/events/299816807>  
    <https://meetup.com/lispnyc/events/300147829>

#### "Youngness" computations:
```apl
      ⍳⍤≢⍛,young
[
 1  'The Dyalog Road Map'                           'Morten Kromberg'    0
 2  'An APL App End to End'                         'Rich Park'          0
 3  'Migration Tools for APL Systems'               'Morten Kromberg'    0
 4  'Parsing User Input for Database Normalisation' 'Kori Smith'         1
 5  'Parsing User Input for Database Normalisation' 'Mark Wolfson'       0
 6  'APL Primitives in the 21st Century'            'Asher Harvey-Smith' 1
 7  'Enhancements in Dyalog v20.0'                  'Asher Harvey-Smith' 1
 8  'Consuming REST APIs in APL with OpenAPI'       'Holden Hoover'      1
 9  'Jarvis and AI'                                 'Brian Becker'       0
 10 'AVG – A Voxel Game'                            'Kyle Croarkin'      1
 11 'The APL Trust – Update'                        'Mark Wolfson'       0
]
      (⊢⌿,⍥(+⌿)(≠⊣⌿))⍉young     ⍝ presentations / total
5 10
      (+⌿,≢)⊢/∪0 1↓young        ⍝ speakers      / total
4 8
```

```bqn
   (⊢˝∾○(+´)·∊⊣˝)⍉young         # presentations / total
⟨ 5 10 ⟩
   (+´∾≠)⊢˝˘⍷0‿1↓young          # speakers      / total
⟨ 4 8 ⟩
```

```k
um:=/(!#:;?/(::;::)@\:)@\:
(+/'(*|:;um@*:)@\:)@+young      / presentations / total
5 10
(+/;#:)@\:(*|)'?1_'young        / speakers      / total
4 8
```

```j
   (([:>]/),&:(+/)([:~:[/))|:young      NB. presentations / total
5 10
   (+/,#)>]/"1~.0 1}.young              NB. speakers      / total
4 8
```

Uiua: left as an exercise `;)`
