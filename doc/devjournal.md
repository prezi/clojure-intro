# Which terminal cast site to use?

I tried shelr.tv first, because you can change its playback speed.  But
I coulnd't log in either with my github, or my twitter account.  So I
couldn't generate an API token which is needed to upload a recording.
There were some problems with sound recording using Sox on OSX, but
that's not crucial.

Then I tried asciinema.org.  I don't like that it uses its own recorder
and format.

I tried playterm.org at last.  It uses plain old `ttyrec` which is good,
but it doesn't handle colors, only black-and-white.  It doesn't handle
backspace, but leaves weird characters instead.  No reference to its
source.  No good at all, out of question.

# "Coverpage" of a screencast

I think it matters.  Remember to have it, for example with
`cowsay` or `figlet`.  The order of steps is

  1. Display cover
  2. Start recording
  3. Start actual performance

# Length of a recording

It may take longer than expected.  Have a way to estimate it.  A
pageful (cca. 32 lines) of code takes 2-3 minutes to type in.

It's also useful to think in terms parts of a presentation, like a
full 10 minute screencast can have a number of "chapters".  You
can separate chapters using some movie-style cut, for example a
`reset`.

# Writing on something that's not part of my daily routine

It takes longer, a lot longer.  Even if I knew quite some bit
about Midje testing and I've used it for some time, it still
doesn't work without me having to read and think about it.  So it
may take even twice as much time.
