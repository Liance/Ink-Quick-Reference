# Ink Quick Reference Sheet

---

### Varying Text

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
He told me a joke. {!I laughed politely.|I smiled.|I grimaced.|I promised myself to not reanct again.}
```
- **~ - Shuffles**: randomised output.
```
I tossed the coin. {~Heads|Tails}.
```
#### Useful features for Varying Text
- **Blank elements**: `{'Wait for it...|||||I am here!'}`
- **Nested elements**: `Ann {waits patiently|{~sighs|shakes her head} and {&glances at her watch|stares exasperatedly at the ceiling|paces about the room}.}`
- **Divert statements**: `I {read the first few chapters.|passed the midpoint of the story.|hit the climax.|finished the epilogue.|finally put the book down. -> finding_next_book}`
- **Choice text variability**: `+ "[Hello {~there|General Grevious}!]`, or if starting with {, use **\** - `+ \ {&Hello there!|Hello there!|You were my brother Anakin!|You were my brother Anakin!} []`

Alternatives can be used inside loops to create the appearance of intelligent, state-tracking gameplay without particular effort.

---
### Conditional Text

Text that varies based on logic.

```
You pack up your things and {met_ryuji.made_friends: go to meet Ryuji at the arcade|head home}.
```
<details><summary>...</summary>
<p>

#### Full Example

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
