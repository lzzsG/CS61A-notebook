and we can play a note
the c note from the beginning
and let's make it a quarter note
all right
mostly silence with little beep at the beginning
and what if we want two beeps
well then we'd play both
the c which is a quarter note at the beginning
and an e which is
starts after a half a second
and lasts for a half a second
I run my code again and listen to the song
now we're getting somewhere
but notice it sounded a little harsh
at the beginning and end of each note
almost a little scratchy
I don't know if that comes through in the video
but it's an important part of making music
that you make each note sound right
the way we'll fix that is just to add a little
fade at the beginning in the end
just for a hundredth of a second
we'll have the amplitude increase and then decrease
so if it's the case that
seconds is less than start plus the feed in time
then what we're going to do is compute the difference
between seconds and the start
so that's how far into the sound were it
and we'll divide by the fade length
to get a percentage of the fade
and we'll multiply that by fft
if it's time to fade out
that's when seconds is greater
then end minus the fade
we can figure out how much is left
and minus seconds
divide that by the fade time
and multiply by the amplitude
so that means we'll fade in and then we'll fade back up
in order to hear the effect
maybe we'll make our fade length a little bit longer
how about 0.1 seconds
but to make it sound as natural as possible
we'll do a really short fate
so it's like the note is starting up right away
but we don't get any weird artifacts in the sound
two nice clean beeps
let's add some more
I'm gonna keep track of how far we are into the song
starting with zero
my first note will be
starting right there at c
I'll play an e
and I'll play it for
just an eighth of a second
okay
now I'll move forward in time by an eighth of a second
and then I'll keep the song that I have
already and add another note
how about another e starting where I am now
this time it's an 8th note
but after it I'm not going to play
another note for a quarter of a second
that means I have an 8th note followed by an 8th wrist
I'll do that again
and then have an 8th note that has no rest after it
and now I think it's time for another note
and like let's make this one a c
followed by an e
so how much time have we used up in total
there's three quarters
and two more eighths makes a whole 2nd
we have 2 seconds according to the
length of the song that we defined in the beginning
so let's add a couple more notes
how about a g
for a quarter and have a little bit of rest after that
and then another g but this time let's make a low g
the way you reach a low g
is just to define the frequency in half
so I'll make a triangle wave for g's frequency
and then a triangle wave
for g's frequency divided by two
and instead of playing these two notes
we're gonna play our whole song
alright so we have the beginning of the mario theme
just as one note at a time
but remember we could play chords
here's a way to make chords
I'm going to put all of this into a function
the mario function needs to know
which CEG and low g it's going to use
and then it will return the song that's generated
instead of committing to a particular ce g and low g
will play mario at a particular octave
and the way you set the octave is just to multiply
the octave by the frequency
so if the octave says
go one octave above will write that is two
which multiplies all the frequencies by two
or if we want to drop an octave
then we'll just divide by two
or multiply by one half
so how do we make a song
when we have local name
ceg and loe g will call mario on those
which might be different
depending on what octave was passed in
and now we could play mario at different octaves
mario at one is what we heard before
mario at one half
plays it in octave down
and of course
since we're representing these functions
and we can combine functions in any way we want
we can play both
mario at one and mario at one half together
and that's how you make music using a computer
all by defining functions
building some elaborate function built out of both and
try combined together in lots of interesting ways
and then we pass that function into play
and it just calls that function on every value of t
rights at the result to a file
and that's how we have a saw