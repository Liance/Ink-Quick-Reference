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
