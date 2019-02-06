# Ink Quick Reference Sheet

> This document aims to be a somewhat more concise reference for writing in Ink. It should be easy to find specific Ink features within this document, with collapsible, fully functional code examples given where correct implementation is either non-obvious or non-trivial.<br>Philosophies governing language design decisions and in-depth explanations of features remain outside the scope of this document but are available in the main [Ink documentation](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md). There will be parts in this document where that rule is broken: usually when a feature is deemed to be confusing without further explanation, and an adequate explanation is missing from the original docs.

>TODO: Possibly in a separate doc - might it be worth building a document that's just useful patterns for commonly occurring gameplay?

## Table of Contents

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Ink Quick Reference Sheet](#ink-quick-reference-sheet)
	- [Table of Contents](#table-of-contents)
	- [1) Basics](#1-basics)
		- [Include](#include)
		- [Text](#text)
		- [Comments](#comments)
		- [Choices](#choices)
		- [Knots and Stitches](#knots-and-stitches)
	- [2) Alternative or Varying Text](#2-alternative-or-varying-text)
		- [Useful features for Alternative Text](#useful-features-for-alternative-text)
		- [Conditional Alternative Text](#conditional-alternative-text)
			- [Conditional Alternative Text Example](#conditional-alternative-text-example)
	- [Variables and Logic](#variables-and-logic)
	- [Lists (Sets)](#lists-sets)
	- [Enabling Non-Linear Structures](#enabling-non-linear-structures)
		- [Tunnels](#tunnels)
		- [Weaves](#weaves)

<!-- /TOC -->

## 1) Basics

### Include
Ink scripts can be split across multiple files with an include statement at the top of the main file: namespacing remains the same and they are still effectively one file in practice, but this allows for easy compartmentalization.
```
INCLUDE newspaper.ink
INCLUDE cities/vienna.ink
INCLUDE journeys/orient_express.ink
```
### Text
Everything that isn't part of the Ink syntax is automatically printed as story text. Text on separate lines produces new paragraphs.

```
Hello!
I'm curious as to why people like saying this but, well -
Hello, world!
```

### Comments
Ink comments are no different than comments in any other language.
```
// This is a comment.

/*
    This is a theoretically unlimited comment block.
*/

TODO: This will print out the written message during compilation, but will not produce anything in the course of actual play.
```

### Choices
Choices allow for player input.
- **Basic choice**: a choice is indicated by an asterisk \*.

```
You briefly consider how to greet the person.
* Hello there!

```
- **Suppressed **

### Knots and Stitches
>TODO

---

## 2) Alternative or Varying Text

Sometimes the same text will be shown multiple times within the same playthrough: when this happens, we can vary it and use **alternatives** to add flavor or reflect a dynamic game world.

Alternatives can be used to build loops that create the appearance of intelligent, state-tracking gameplay without particular effort.

- **| - Sequence**: iterates until the final element.
```
{"Three!"|"Two!"|"One!"|"Action!"|The set is live, everybody is busy filming.}
```
- **& - Cycle**: iterate and loop content.
```
It was {&Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Sunday} today.
```
- **! - Once-only**: iterates until final element, then displays nothing.
```
He told me a joke. {!I laughed politely.|I smiled.|I grimaced.|I promised myself to not react again.}
```
- **~** - **Shuffles**: randomised output.
```
I tossed the coin. {~Heads|Tails}.
```

### Useful features for Alternative Text

- **Blank elements**:`{'Wait for it...|||||I am here!'}`
- **Nested elements**: `Ann {waits patiently.|{~sighs|shakes her head} and {&glances at her watch|stares exasperatedly at the ceiling|paces about the room}.}`
- **Divert statements**: `I {read the first few chapters.|passed the midpoint of the story.|hit the climax.|finished the epilogue.|finally put the book down. -> finding_next_book}`
- **Choice text variability**: `+ "[Hello {~there|General Grevious}!]`: if starting with {, use **\** to escape the brackets otherwise it will be read as a conditional.

<details><summary>Blank elements example</summary>
<p>

```
-(top)
A man with ridiculously large muscles is posing in front of you.
{"Wait for it..."|||||"I am here!\"->END}
+[You wait around for a bit] ->top
```
</p>
</details>

<details><summary>Nested elements example</summary>
<p>

```
-(top)
    Ann {waits patiently|{~sighs|shakes her head} and {&glances at her watch|stares exasperatedly at the ceiling|paces about the room}.}
+ [You tell Ann to wait just a little bit longer...] ->top
```
</p>
</details>


<details><summary>Divert statements example example</summary>
<p>

```
-(top)
    I {read the first few chapters.|passed the midpoint of the story.|hit the climax.|finished the epilogue.|finally put the book down. -> END}
+[You kept reading -] ->top
```
</p>
</details>
<details><summary>Choice text variability example</summary>
<p>

```
-(top)
    + \ {&Hello there!|Hello there!|You were my brother Anakin!|You were my brother Anakin!} [] ->top
```
</p>
</details>


### Conditional Alternative Text

Text that varies based on logic.

```
You pack up your things and {met_ryuji.made_friends: go to meet Ryuji at the arcade|head home}.
```
<details><summary>Full example.</summary>
<p>

#### Conditional Alternative Text Example

```
-> school

=== school
    You make it through another day of school.
    * [Head out into the corridor] -> met_ryuji
    + You pack up your things and {met_ryuji.made_friends: go to meet Ryuji at the arcade|head home}.
    {met_ryuji.made_friends: -> arcade|->home}

=== met_ryuji
    A scruffy looking punk greets you in the corridor.

    "Hey, I'm Ryuji!"
        * [Return the greeting in a friendly manner.]
        -> made_friends

=made_friends
    You and Ryuji are friends now!
    * [Next day of school] -> school


=== arcade
    You spend the rest of your day hanging out with Ryuji at the arcade.
    +[Before you know it, it's time for another day of school.]
    ->school


=== home
    You spend the rest of your day sulking about at home, wasting away the evening on your phone.
    +[Before you know it, it's time for another day of school.]
    ->school
```

</p>
</details>

---
## Variables and Logic
>TODO
## Lists (Sets)
>TODO
## Enabling Non-Linear Structures
>TODO
### Tunnels
>TODO
### Weaves
>TODO
