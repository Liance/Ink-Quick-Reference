# Ink Quick Reference Sheet

> This document aims to be a somewhat more concise reference for writing in Ink. It should be easy to find specific Ink features within this document, with collapsible, fully functional code examples given where correct implementation is either non-obvious or non-trivial.<br>Philosophies governing language design decisions and in-depth explanations of features remain outside the scope of this document but are available in the main [Ink documentation](https://github.com/inkle/ink/blob/master/Documentation/WritingWithInk.md). There will be parts in this document where that rule is broken: usually when a feature is particularly confusing without further explanation, and an adequate explanation is missing from the original docs.

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
	- [3) Variables, Functions and Logic](#3-variables-functions-and-logic)
		- [Using Variables and Constants](#using-variables-and-constants)
		- [Using Functions](#using-functions)
		- [Calling External C# Functions](#calling-external-c-functions)
	- [4) Lists (Sets)](#4-lists-sets)
	- [5) Enabling Non-Linear Structures](#5-enabling-non-linear-structures)
		- [Tunnels](#tunnels)
		- [Weaves](#weaves)

<!-- /TOC -->

---

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

- **+** -**Sticky choice**: by default, choices indicated with an \* are "used up" once they're selected, so even if the flow comes around to the same choice, previously selected choices won't be shown anymore. using a + symbol instead of an * means that the choice won't get "used up", even after it's chosen.

```
=== homers_couch ===
	+	[Eat another donut]
		You eat another donut. -> homers_couch
	*	[Get off the couch]
		You struggle up off the couch to go and compose epic poetry.
		-> END
```
<details><summary>Some of the above syntax may be unfamiliar at this point - click here for an explanation and the full output.</summary>
<p>
The === denotes a [knot](knots-and-stitches), which is how Ink structures sections of content. `-> homers_couch` is a [divert]

```

```
</p>
</details>



<br>- **[ ]** - **Suppressed** choices hide their text once they are selected. Everything within the square brackets will not be printed into response.

```
Hi there!
* [Return their greeting. This choice text won't be printed after it's selected.]
	Hello back!
```

<details><summary>The resultant output.</summary>
<p>

```
Hi there!
1: [Return their greeting. This choice text won't be printed after it's selected.]

>1
Hello back!
```
</p>
</details>

<br>Suppressed choice text can be mixed with normal choice text. The square brackets act as dividers within the choice content when this is the case.

Content before the square brackets is printed in both choice selection and output; content inside is printed only during choice selection; content after is only printed in the output.

```
"Do you want to go fishing after school?" Ryuji asks.

	* I [hate fishing, but I don't want to hurt Ryuji's feelings.]have some chores to run today, sorry, is what you end up saying.

		Ryuji slaps you on the back affably and shakes his head as if to say never mind. "Maybe some other day, then."
```

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

**Conditional Alternative Text Example**

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

## 3) Variables, Functions and Logic
>TODO
### Using Variables and Constants
>TODO
### Logic queries
>TODO
### Math
>TODO
### Using Functions
>TODO
### Calling External C# Functions
>TODO

---

## 4) Lists (Sets)

>Technical pre-amble: Lists in Ink are effectively sets: they guarantee uniqueness, have operations like union and intersection, and are fundamentally written as dictionaries behind-the-scenes. They are named Lists and not Sets only because writing stuff like "Set the Set" gets very confusing, very fast.

>TODO

---

## 5) Enabling Non-Linear Structures
>TODO
### Tunnels
>TODO
### Weaves
>TODO
