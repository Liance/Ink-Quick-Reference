# Ink Quick Reference Sheet

> This document aims to be a somewhat more concise reference for writing in Ink. It should be easy to find specific Ink features within this document, with collapsible, fully functional code examples given where correct implementation is either non-obvious or non-trivial.

### Varying Text

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
<details><summary>...</summary>
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
