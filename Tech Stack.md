A quick, easy option if you want to make an AR character with some animation and lip sync ability tied to the character’s speech output is to use Unity, with the following tech stack:

Spirit Character Engine + SALSA + RTVoice + ARCore + Unity

Getting Started
1. To get started with Unity & ARCore, you need the latest version of Unity (2017.2+) and the Android 7+ SDK (API level 24 or higher). For more information on this, you can read this official Google quickstart for Unity.
Also, download the ARCore SDK for Unity.
2. Create a new Unity 3D project and import the ARCore SDK for Unity .unitypackage file by clicking the menu Assets > Import package > Custom Package and import everything in the Unity package.
3. Once you know the location of your project on disk, export your project from your Character Engine Authoring Tool, by pressing the ‘Export’ button in the menu. First, make sure your Project Settings are set to export to a StreamingAssets folder in your Unity project.

4.Set up your project for Character Engine according to the instructions in your Spirit documentation — this is currently limited access to existing beta clients, but you can also sign up for Beta access now.

5. Next, the rest of the ARCore setup can be found here: https://developers.google.com/ar/reference/unity/

6. Finally, the SALSA integration is quick and easy — you can download the SALSA with RandomEyes with LipSync from the Unity Asset Store.

7. Install SALSA with RandomEyes into your project by importing from the asset store straight into your project.

8. Install RT-Voice. You can download it from the Unity Asset Store here: https://www.assetstore.unity3d.com/en/#!/content/41068

9. Import the SALSA with RandomEyes RT-Voice support package (Salsa_RTVoice). Select [Assets] -> [Import Package] -> [Custom Package…] and Browse to the [Salsa-RTVoice_1.0.0.unitypackage] file and [Open].

10. Set up a SALSA 2D or SALSA 3D enabled visual character. The SALSA integration is quick and simple — the SALSA 2D or SALSA 3D AudioSource just needs to be set to the RTVoice (TTS) plugin GameObject/AudioSource. SALSA takes care of the rest.

---

Stories in games are still largely representable as static graphs.

>A changeful tale is a dream of a particular aesthetic for interactive stories: one where with each traversal — each unique pathway through the work — the player can exhibit enough agency to craft something that feels meaningfully their own.

>Sam Barlow’s design work on Her Story was certainly about composing a sequence of possibilities; so too do the designers of Fallen London or Dungeons & Dragons work, in different ways, to conduct you through a space of potential fictions.

>We can call a system’s processes expressive if authorial intent can be recognized in them.

> Storygame -
**a playable system** with
**units of narrative**, where
the **understanding of both system and narrative**, and the relationship between them, enables a traversal through the work.

>Compare this to a game like the original Super Mario Bros [...] While this narrative content might contextualize, motivate, or comment on the gameplay, actually understanding it is not required for a satisfying traversal.

> Its potentialities are not easily enumerable, and its possibility space large enough that a player might rightly feel a sense of discovery, surprise, or even ownership over their input.

Given a character creator with 5 skills and a pool of stat points to distribute among those skills - the range of outcomes may not be immediately obvious, some inputs may even surprise the system's designer, and it is difficult or impractical or impossible to enumerate all of the possible inputs as a comprehensive list of options.

>It’s important to note that expressive input does not require a corresponding expressive process under the hood. The RPG attached to Skill Creator might not actually implement all of the listed skills; or perhaps no matter what skills the player picks, all outcomes are determined at random, because of a bug or even intentional design. This does not change the input’s perceived expressiveness.

>Of course, the player is likely to be disappointed if their expressive input is ignored, one of several reasons why expressive input is not always a good idea nor inherently superior to alternatives. Overwhelming the player with perceived agency can lead to frustration, especially if there are actually only a few — or one! — correct courses of action. This is the classic pit trap of the adventure game.

>a space in which discoveries can be made

>In a well-designed system, the player quickly comes to understand its relevant logics: the way in which interacting with it causes consistent changes to the player’s mental model of its simulated world. Imagine a degenerate Myst, where the click targets were scrambled. Each click on a view takes you to a seemingly unrelated image. On a technical level, this is no different at all from the canonical Myst, but the logic of movement has been broken: the player would have no sense of moving through a connected world, and the sequence of images really would feel like a slideshow, rather than a simulation of space.

Narrative Mechanics -

1. Story dumps. The player can activate something to reveal a particular (or random) lexia. (Audio recorders strewn around a level; an NPC with random barks.)

2. Explicit story choice. The player is given a list of alternatives, and is shown a different lexia next depending on their choice. (Choose Your Own Adventure; dialogue trees.)

3. Delayed story choice. The player makes a decision that effects which lexia they see at a later point. (Picking a class in an RPG; moving a good/evil bar.)

4. Challenge-gated content. The player must use unrelated mechanics to achieve a particular victory; doing so successfully reveals new lexia. (Beating a platformer level to get the next cut scene; solving a puzzle.)

5. Naming. The player directly chooses or enters text that becomes incorporated into future lexia. (Asking for the player’s name.)


Narrative Logics - operable story machines.

- Story as Coin-Op Reward — do the right action, get a piece of story. The action might be as simple as bumping into an NPC, or as complex as completing a sequence of boss fights.
- Story as Navigable Graph — as in a Twine, an adventure game’s map of connected rooms, or a dialogue tree; a space the user can move through (freely or with restrictions) where each node has story content as well as connections to more story content.
- Story as Fleeting Opportunities — chances to get new story content come and go based on the changing game state (characters coming and going on a schedule; actions becoming available when a flag or stat reaches a certain value).
- Story as Recurring Variations—repeatedly getting a variant on one or more recurring stories, as with procedurally generated or templated quests.

>Games of social simulation (like Prom Week, Redshirt, or Blood & Laurels) strive toward the ambitious goal of a narrative logic that feels like interacting with a person, such that common-sense ideas like treat this person poorly and they’ll get mad at me become as actionable as click next to continue. But players aren’t familiar with logics this complex, and designers have neither established patterns of system-building nor conventions of UI to fall back on. These games can risk feeling unsatisfying, frustrating, or even broken, despite their revolutionary technology.
