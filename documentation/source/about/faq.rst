.. _faq:

Frequently Asked Questions
==========================

General
-----------

How do I ask a question so that it becomes frequently asked?

    Don't you hate FAQs that are not based on anything anyone's ever asked?  
    To ask, post to https://groups.google.com/g/music21list.  
    But first read what we've already come up with below.

Why is it called `music21`?

    `music21` gets its name from the fact that it was (mainly) created at
    MIT in the Music and Theater Arts Section there.  At MIT, everything
    has a number, and the department number for music is 21M.  There's
    no connection to "Twenty-first century" etc. and therefore superior
    to older software. In fact, if I had thought of that mental connection 
    I probably would have come up with a different name.
    
    There was a tradition early on of naming software that dealt with
    music, with "MUSIC" followed by a number (https://en.wikipedia.org/wiki/MUSIC-N).      
    There is famously Max Matthews'
    MUSIC II, III, and IV (the sequels to just plain "MUSIC"), 
    MUSIC V (Matthews and Miller),
    MUSIC 360 and MUSIC 11 (Vercoe et al., which became CSound).  
    These systems were originally created to synthesize sound digitally
    though their successor systems can do quite a number of different things.
    
    I figured that since no one had actually released a piece of software
    in over 35 years that actually followed the "Music N" naming structure,
    it was fair game to think of it not as the paradigmatic name just for a
    software synthesis package, but for any new or original usage of software
    and music.  
    
    I'm pretty tickled that the new naming convention is getting an homage
    in Anas Ghrab's music22 package: https://pypi.org/project/music22

    When I was giving a talk in Germany, everyone referred to it as
    Musikeinundzwanzig, and that made me happy, so feel free to localize
    the name however you like when speaking in your language.
    Musique vignt-et-un, 音楽二十一, whatever.
    
What is the native `music21` data format?

    Quick answer: There is none, but it doesn't matter.

    Longer answer: `music21` is a toolkit for the manipulation and analysis of data 
    that you already have or are generating on the fly. As such, its strength is its (and python's) 
    ability to work with many common formats and easy extensibility to work with many more. 
    You will find that for the most part you will not need to preserve your 
    `music21` data in an interchangeable format. And the number of things you can do 
    with `music21` makes it impossible for us to create formats for every possible use. 
    We work with `music21` all the time for our work and have never needed one.
    
    But if you must store your `music21` data somehow, here are some suggestions:
    
    * For data that can quickly and exactly be recreated, 
      use the script that generates as your data storage.  
      Then just rerun the script to get your data back.

    * For storing music notation, musicXML output will work well for many purposes. 
      If you just want to store an 
      audio file or graphic of your output, MIDI or Lilypond->PNG could work.

    * For data that cannot easily be recreated (because it's computationally expensive to create, or 
      relies on user input, or is stochastically generated), 
      Python's pickle package will allow you 
      to store your data on disk.  These files cannot necessarily 
      be read in by a later version of `music21` 
      (This is the reverse of the problem Finale has, 
      where you can only read older versions of files), so it 
      should not be used for long term storage and sharing.  
      Run `s.freeze()` and then `s.thaw()` later.  Or for more deeply configurable
      needs, :meth:`~music21.stream.Stream.setupSerializationScaffold` and
      :meth:`~music21.stream.Stream.teardownSerializationScaffold` 
      before running `pickle.dump(yourStream)` and
      after running `pickle.load(yourStream)` 
      respectively and almost everything will be preserved. 

    * For data that cannot easily be recreated but needs long-term storage and sharing, 
      try saving the relevant 
      parts of the data in an XML, json, or even CSV(!) format. 
      See plistlib at https://docs.python.org/dev/library/plistlib.html
      or https://code.activestate.com:443/recipes/440595. You cannot store every 
      element of python's object structure, 
      but you should easily be able to store the parts that are difficult to recreate. 
      `Music21` has some facility for a JSON storage of Streams, but it is not complete.

    * If you're programming data structures too complex to be encapsulated 
      in one of the solutions above, 
      you should have enough experience to create a data storage format of your own. 
      Please consider contributing 
      your solution to improve the package.

I'm ready to give it a try, but how do I install `music21`?

    Please see the complete install instructions: 
    :ref:`User's Guide, Chapter 1: Installing music21 <usersGuide_01_installing>`.

I'm using Linux/GNU/Unix and I'm having trouble configuring `music21`, can
you help?

    Unfortunately, due to the number of different flavors of open-source
    operating systems, the development team can only give free help to
    Mac and Windows installation. (but see paid support, below).

Uses
---------
Can I synthesize new sounds with `music21`?

    Yes, and no.  `Music21` is primarily built for manipulating symbolic
    musical data not sound waves.  There are lots of great programs for
    doing that.  But the symbolic data, however, can be used as data within
    a large variety of synthesis packages. So you could create new
    `music21` objects that control the synthesis package of your choosing.

Can `music21` read in music directly from an image or a .pdf?

    Sorry, that's beyond `music21`'s capabilities. This technology
    is called OMR (Optical Music Recognition) and it's a whole separate
    field of research in itself.  Audiveris is an open-source OMR
    software toolkit.  The development team here has had good experience
    with the commercial SmartScore application.  `Music21` does have a
    good set of modules for improving the output of OMR after it's done.
    See :ref:`moduleOmrCorrectors`.

I'm having trouble reading in MIDI.  The docs for `music21.midi.translate`
and `music21.converter.subConverters.ConverterMIDI` are rather hard
to understand.  (Same for `musicxml`, `mei`, etc.)

    You shouldn't need to be going into subConverters or the various format
    modules, like `music21.midi` or `music21.musicxml` in everyday use.
    Just load the file into the system with `music21.converter.parse(filename)`
    and it will figure out the right format and everything else, and give you
    a `Stream` object.  To load
    from the internet, you can pass in a URL instead.  If
    `filename` does not give enough information to determine the file type,
    add `format='midi'` and it will do the right thing.

    To save a `Stream` (stored as variable `s`) afterwards, just call:
    `s.write('midi', fp='filename.mid')`.  Or to hear it immediately,
    `s.show('midi')`.


Feature requests and Consulting
-------------------------------
`Music21` doesn't have some feature that I need, how do I get it added?

    It won't hurt to email the list (or us directly) and we'll consider it.
    However, we do have a priority list based on what we think the widest
    audience will require or what we need for our own research.  If you'd
    like your request to leap-frog to the front of the line, the best way
    is to endow the programming of your feature through a donation that will
    enable us to increase the number of student programming assistants we
    employ.  (Or side-step us and offer a cash bounty on the music21list
    itself).

No, you don't understand, I **really** need this feature!

    If you really need something done in `music21`, we offer paid support
    by the hour at standard consulting rates. Contact `michael.asato.cuthbert@gmail.com`
    for details and rates.
    
Is this also what I should do if I need help using `music21` for my own project?

    Yes, if you're having trouble getting `music21` to do what you want and you've
    tried the mailing list/StackOverflow, etc. consulting is available to help.
    
Why not put the rate here?

    The rate varies according to the difficulty of the feature--whether it
    requires a principal investigator to run or whether it could be incorporated
    into the education of a student; whether licensing agreements need to be signed, etc.
    
    Discounts are available for
    academic researchers/composers who consider the consultation sufficiently 
    essential as to add
    authorship credit to the development team on a publication. 


3rd-Party Utilities
--------------------

What is MusicXML?

    MusicXML is a file format for exchanging musical scores among different 
    programs, such as, oh... `music21` and Finale (or `music21` and Sibelius,
    or Dorico, or MuseScore).  
    It was created by Recordare (Michael Good, CEO) and now run by the W3C. More 
    information about the project can be found at:

    * https://www.musicxml.com/

And this Humdrum about which you speak?

    It's another framework for studying music as symbolic data using 
    simple text files and UNIX scripting tools.  Created by David Huron
    in the 80s and 90s. We're big fans of Humdrum 
    here at `music21`, but we thought that it was time to take a 
    different approach. 

    Information on Humdrum can be found here at the following links:

    * https://www.humdrum.org
    * https://kern.humdrum.org


