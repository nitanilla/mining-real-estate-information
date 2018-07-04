
# Simple Movie Organizer

this is a movie organizer that works with files and folders. gets movies information from omdb api. correct the name of folder to match imdb title. sort all movies by year by creating year folders. removes duplicates .

### Usage:
```
usage: organizer.py [-h] [--version] [--dirs [DIRS [DIRS ...]]]
                    [--parents [PARENTS [PARENTS ...]]] [-c] [-p] [-m]
                    [--checkfiles] [-d] [--ask] [--biggest] [--smallest]
                    [--name] [--year] [--directors DIRECTORS DIRECTORS]

a movie organizer

optional arguments:
  -h, --help            show this help message and exit
  --version             show program's version number and exit
  --dirs [DIRS [DIRS ...]]
                        movies are in this directories
  --parents [PARENTS [PARENTS ...]]
                        parent folder where movie dirs are
  -c                    clear database (for debugging)
  -p                    print all movies in database
  -m                    make folders for movies if movie files (i.e, .mp4) is
                        in directory
  --checkfiles          recheck database and files (deleted movies)
  -d                    check duplicate movies
  --ask                 ask every duplicate movie to save which one . must use
                        -d arg
  --biggest             keeps the biggest movie in case of duplicates. must
                        use -d arg
  --smallest            keeps the smallest movie in case of duplicates. must
                        use -d arg
  --name                corrects the name of folder to actual title
  --year                Makes Yearly Folder
  --directors DIRECTORS DIRECTORS
                        Makes Directors shortcut which have more than N
                        movies, first arg is the limit, 2nd arg is path

  --write               write omdb data in movie folder/.omdb
  --read                reads movie data that has been saved with --write
```

### Requirements
* python2.7
* pip install pathlib
* pip install shutil
* pip install unidecode
* mongodb 3.4+
* python mongoclient

### Known Issues
* when there are two movies with same name, manually move the movie to correct folder if its been placed in the wrong year and rerun the code with '--checkfiles' arg.

### Example

```
sudo ./organizer.py --parents "/media/al/My Passport/Movies" -m --checkfiles -d --bigest --year --directors 3 "/media/al/My Passport/Movies/Directors"
```

### Before :
```
.
├── 2011 Movies
│   ├── A.Separation.2011.LiMiTED.720p.BluRay.x264-LPD
│   ├── Cars.2.1080p.Bluray.x264-METiS
│   ├── Contagion.2011.720p.BluRay.X264-AMIABLE
│   ├── Green.Lantern.2011.EXTENDED.720p.Bluray.x264-MHD
│   ├── Hugo.2011.1080p.BluRay.X264-AMIABLE
│   ├── J.Edgar.2011.720p.BRRip.x264.AAC-ViSiON
│   ├── Kung.Fu.Panda.2.2011.1080p.BluRay.x264-SiNNERS
│   ├── Midnight.in.Paris.720p.BluRay.x264-MHD
│   ├── Mission.Impossible.Ghost.Protocol.2011.1080p.BluRay.xnHD.x264-NhaNc3
│   ├── My.Week.With.Marilyn.2011.720p.BluRay.x264.DTS-HDChina
│   ├── Pirates.Of.The.Caribbean.On.Stranger.Tides.720p.BluRay.x264-REFiNED
│   ├── Real.Steel.2011.720p.BluRay.x264-REFiNED
│   ├── Sherlock.Holmes.A.Game.Of.Shadows.2011.720p.BluRay.x264-SONS [PublicHD]
│   ├── The.Adventures.of.Tintin.2011.720p.BluRay.x264-MHD
│   ├── The.Descendants.2011.720p.BluRay.x264-ALLiANCE
│   ├── The.Girl.With.The.Dragon.Tattoo.2011.720p.BluRay.x264-SPARKS
│   ├── The.Hangover.Part.II.2011.720p.BluRay.x264-Felony
│   ├── The.Help.2011.720p.BluRay.x264-Felony
│   ├── The.Ides.Of.March.2011.720p.BRRip.XviD.AC3-ViSiON
│   ├── The.Muppets.2011.720p.BluRay.x264-SPARKS
│   ├── The.Rum.Diary.2011.720p.BluRay.x264-SPARKS
│   ├── The.Tree.of.Life.2011.720p.BluRay.x264.DTS-WiKi
│   ├── Tinker.Tailor.Soldier.Spy.2011.720p.BluRay.x264-iNFAMOUS
│   ├── Tower.Heist.2011.720p.BluRay.x264-AMIABLE
│   ├── UNDERWORLD 1-2-3 HD 720p BRRip 5.1AAC x264-ILPruny
│   ├── [ UsaBit.com ] - Moneyball.2011.720p.BRRip.XviD.AC3-ViSiON
│   ├── War.Horse.2011.720p.BRRip.x264.AAC-ViSiON
│   ├── Warrior.2011.720p.BluRay.x264-Felony
│   └── X-Men.First.Class.2011.BluRay.720p.DTS.x264-CHD
├── 2012
│   ├── 21 Jump Street (2012)
│   ├── Chronicle (2012)
│   ├── Dark.Shadows.2012.720p.BluRay.x264.DTS-HDChina [PublicHD]
│   ├── John Carter 2012 BRRip 720p x264 AAC - KiNGDOM
│   ├── Lockout.UNRATED.720p.BluRay.x264-BLOW [PublicHD]
│   ├── Men.in.Black.3.2012.720p.BluRay.x264.DTS-HDChina [PublicHD]
│   ├── Prometheus.2012.720p.WEB-DL.DD5.1.H.264-CtrlHD [PublicHD]
│   ├── Safe.House.2012.720p.BRRip.XviD-HiGH
│   ├── Snow.White.and.the.Huntsman.2012.EXTENDED.720p.BluRay.X264-AMIABLE [PublicHD]
│   ├── The.Avengers.2012.1080p.BluRay.x264-Rx [PublicHD]
│   ├── The.Cabin.In.The.Woods.2011.720p.BluRay.x264-HDEX [PublicHD]
│   ├── The.Dark.Knight.Rises.2012.1080p.BluRay.x264-ALLiANCE
│   ├── The.Dictator.2012.UNRATED.720p.BluRay.X264-AMIABLE [PublicHD]
│   ├── The.Expendables.2.2012.iNTERNAL.720p.BluRay.x264-AVSHD [PublicHD]
│   ├── The.Hunger.Games.2012.1080p.BluRay.x264-BLOW [PublicHD]
│   ├── The.Lorax.2012.720p.BluRay.x264-SiNNERS [PublicHD]
│   ├── [UsaBit.com] - Project.X.2012.EXTENDED.720p.BRRip.XviD.AC3-REFiLL
│   └── Wrath of the Titans (2012)
├── Moveis_2
│   ├── Captain America: Civil War
│   ├── Fanny and Alexander
│   ├── Goodfellas
│   ├── Manhattan Murder Mystery
│   ├── Match Point
│   ├── The Turin Horse
│   └── Wild Strawberries
├── movie
│   ├── About Elly
│   ├── Exit Through the Gift Shop
│   ├── Hidden Figures
│   ├── Hitchcock Truffaut
│   ├── King Kong
│   ├── Life+1Day
│   ├── Lion
│   ├── Magic Mike
│   └── The Boy Friend
├── MoviE
│   ├── 12 Angry Men 1957 HDTVrip 720p x264 [Herakler]
│   ├── 2 Guns 2013 720p WEB-Rip  x264 AAC KiNGDOM
│   ├── 300 Rise of an Empire 2014 720p BRRip H264 DTS 5.1 - KiNGDOM
│   ├── A.Better.Tomorrow.1986.x264.DTS.2AUDIO-WAF
│   ├── A.Better.Tomorrow.2.1987.x264.DTS.2AUDIO-WAF
│   ├── Afflicted 2013 720p BRRip x264 AAC-JYK
│   ├── Alice in Wonderland
│   ├── Anchorman - The Legend of Ron Burgundy (2004)
│   ├── Apocalypse_Now_{1979}
│   ├── A.Serious.Man.2009.LIMITED.1080p.BluRay.x264
│   ├── Avatar.2009.1080p
│   ├── Back To The Future (Trilogy)
│   ├── Batman Begins (2005) [1080p]
│   ├── Before.The.Devil.Knows.You're.Dead[2007]DvDrip[Eng]-aXXo
│   ├── Behind The Candelabra 2013 720p BRRip x264 AC3-JYK
│   ├── Blade.Runner.Final.Cut.1997.720p.BluRay.x264-WiKi
│   ├── Blue Jasmine 2013 1080p BDRip H264 AAC - KiNGDOM
│   ├── Blue Valentine 2010 720p BRRip H264 AAC-GreatMagician (Kingdom-Release)
│   ├── Boogie Nights (1997)
│   ├── Borat
│   ├── Bourne 1,2,3
│   ├── Charly
│   ├── Children of Men [2006] 720p BRRiP x264 AAC - ExtraTorrentRG
│   ├── City of Gods
│   ├── City Slickers 1991 1080p BDRip H264 AAC - KiNGDOM
│   ├── Cloud Atlas 2012 BRRip 1080p x264 AAC - KiNGDOM
│   ├── Cloudy with a Chance of Meatballs 2 (2013)
│   ├── Conan The Destroyer 1984 BRRip 1080p x264 AAC - (Kingdom Release)
│   ├── Cronos 1993 BRRip XvidHD 720p-NPW
│   ├── Disney's Hercules 1997 1080p BDRip H264 AAC - KiNGDOM
│   ├── Don't Be Afraid Of The Dark 2010 BDRip 1080p x264 AAC - KiNGDOM
│   ├── Elysium.2013.720p.BluRay.DTS.x264-DNL
│   ├── Enders.Game.2013.720p.BluRay.DTS.x265.HEVC-PublicHD
│   ├── Enemy.2013.1080p.WEB-DL.H264-PublicHD
│   ├── Escape.Plan.2013.720p.BRRip.x264.AAC-ViSiON
│   ├── Eternal Sunshine of the Spotless Mind (2001)
│   ├── Evil Dead 2013 720p BRRIP  x264 AAC KiNGDOM
│   ├── Exorcist
│   ├── Fear And Loathing In Las Vegas 1998 720p x264 BRRip GokU61[Z Warriors Release]
│   ├── Finding.Nemo.x264.720p-HR
│   ├── Frankenweenie 2012 BDRip 720p x264 AAC - KiNGDOM
│   ├── Frozen (2013)
│   ├── Goodbye Mr. Chips (1969)
│   ├── Good Morning Vietnam 1987 1080p BDRip H264 AAC - KiNGDOM
│   ├── Guess Who's Coming To Dinner.Sidney Poitier.Audrey Hepburn.DvdRip-Munchkinoid
│   ├── Hardware (1990) 1080p
│   ├── If.... (1968) Criterion BDRip 720p AAC multisub HighCode
│   ├── In.Bruges.2008.720p.BluRay.DTS.x264-ESiR
│   ├── Incendies 2010 SONY BDRip 720p DTS multisub HighCode
│   ├── Inception
│   ├── Indie.Game.The.Movie.2012.720p.WEBRip.x264-WaLMaRT
│   ├── Inglouries Bastards
│   ├── In the Mouth of Madness 1994 1080p BDRip H264 AAC - KiNGDOM
│   ├── Into The Wild (2007)
│   ├── Jackass 3D 720p
│   ├── Jackass Presents Bad Grandpa (2013)
│   ├── Joe.2013.1080p.WEB-DL.H264-PublicHD
│   ├── Julie.and.Julia
│   ├── Kill Your Darlings 2013 720p BRRip x264 AC3-JYK
│   ├── Kings Speech
│   ├── LA Confidential {1997} 720p BRRip x264 - HDMiCRO by Mr. KickASS
│   ├── Lawrence of Arabia 1962
│   ├── Liar Liar_1997
│   ├── Little.Miss.Sunshine[2006]DvDrip[Eng]-aXXo
│   ├── LITTLE_WOMEN
│   ├── Lone Survivor 2013 BluRay 1080p x264 DD5.1 FLiCKSiCK
│   ├── Lord of the Rings Trilogy BluRay Extended 1080p QEBS5 AAC51 PS3 MP4-FASM
│   ├── Madagascar 2005 720p BRRip x264-HDLiTE
│   ├── Madagascar.Escape.2.Africa.2008.BluRay.720p.x264.DTS.RoSubbed-WiKi
│   ├── Manhattan.1979.DVDRip.XviD-VLiS
│   ├── Master And Commander The Far Side Of The Earth 720p
│   ├── Memento 2000 BRRip 720p H264 AAC-BeLLBoY (Kingdom-Release)
│   ├── Me Myself and Irene (2000) 720p
│   ├── Monty.Python.and.the.Holy.Grail.1975.1080p.BluRay.x264.anoXmous
│   ├── Monty Python's Life Of Brian[1979]BDrip[Eng]1080p[AC3 6ch]-Atlas47
│   ├── Monty Pythons The Meaning of Life 1983 1080p HDDVDRip H264 AAC - IceBane (Kingdom Release)
│   ├── Mulberry Street 2006 DVDRip XviD AC3 MRX (Kingdom-Release)
│   ├── Mulholland Dr (2001)
│   ├── Mysteric River
│   ├── Network.1976.DVDRip.XviD
│   ├── Nikita 1990 m-720p
│   ├── Non-Stop 2014 720p BRRip x264 AAC-KiNGDOM
│   ├── O Brother, Where Art Thou[2000]
│   ├── Oculus 2014 1080P BDRip H264 AAC - KiNGDOM
│   ├── Only Lovers Left Alive (2013) 1080p x264 DD5.1 EN NL Subs
│   ├── On the Waterfront.1954.DVDRip.x264.AAC[21 multisubs]-BeLLBoY
│   ├── Out of the Furnace 2013 BRRip 720p x264 AAC - KiNGDOM
│   ├── Outrage.2010.BlyRay.720p.DTS.x264-CHD
│   ├── Paranorman 2012 720p BRRip H264 AAC - KINGDOM
│   ├── Philomena.2013.1080p.WEB-DL.H264-PublicHD
│   ├── Pineapple Express
│   ├── Polytechnique.2009.720p.BluRay.DD5.1.x264-PublicHD
│   ├── Princess Mononoke
│   ├── Prisoners 2013 1080p BDRip H264 AAC - KiNGDOM
│   ├── Pulp Fiction 1994 720P BRRip {MnM-RG H264}
│   ├── Rampart 2011 LIMITED 1080p x264 AC3 - KiNGDOM
│   ├── Rendition 2007 1080p BRRip x264 AAC-KiNGDOM
│   ├── Riddick Unrated DC 2013 BDRip 1080p x264 DTS 5.1 - KiNGDOM
│   ├── Road To Perdition 720p
│   ├── Ronin 1998
│   ├── Santa Sangre [BDRip-720p-MultiLang-Sub-Eng-Chapters][RiP By MaX]
│   ├── Scarface (1983)
│   ├── Se7en (1995)
│   ├── Seven Samurai 1954 Restored 720p BRRip x264 AAC-BeLLBoY (Kingdom-Release)
│   ├── Sherlock Holmes
│   ├── Shutter Island
│   ├── Side Effects 2013 BRRip 720p x264 AAC - KiNGDOM
│   ├── Skyfall.2012.1080p.BluRay.x264-DAA
│   ├── Small Soldiers
│   ├── Snatch {2000} 720p BRRip x264 - Mr. KickASS
│   ├── Solomon.Kane.2009.720p.BDRip.XviD.AC3-ViSiON
│   ├── Spirited Away 720p HDTV
│   ├── Star Trek (2009)
│   ├── Take Shelter 2011 LIMITED 1080p BRRip x264 AC3-26K
│   ├── Taxi Driver 1976 720p BRRip H264 AAC-GreatMagician (Kingdom-Release)
│   ├── The.84th.Annual.Academy.Awards.2012.720p.HDTV.x264-2HD
│   ├── The Amazing Spider-Man 2 2014 1080P BDRip H264 AAC - KiNGDOM
│   ├── The Big Lebawski (1998)
│   ├── The Chronicles of Riddick Unrated DC 2004 1080p HDDVDRip H264 AAC - KiNGDOM
│   ├── The Counselor 2013 Unrated Extended 720p BRRIP x264 AAC KiNGDOM
│   ├── The Devil's Backbone 2001 720p BRRip x264 AAC-KiNGDOM
│   ├── The Fifth Estate 2013 720p BRRip x264 AC3-JYK
│   ├── The Fighter 720p
│   ├── The Ghost Writer 720p
│   ├── The.Good.The.Bad.And.The.Ugly.Extended
│   ├── The.Good.The.Bad.The.Weird.2008.DvDRip-FxM
│   ├── The Great Beauty 2013 Blu-Ray 1080p x264 DD5.1 FLiCKSiCK
│   ├── The Hurt Locker
│   ├── The Interview (1080p)
│   ├── The Lego Movie (2014)
│   ├── The Monuments Men 2014 720p BRRip x264 AAC-JYK
│   ├── The.Next.Three.Days.2010.720p.BRRip.XviD.AC3-ViSiON
│   ├── The Other Guys[2010]
│   ├── The Red Line
│   ├── The.Right.Stuff.1983.1080p.BluRay.x264.anoXmous
│   ├── The Road (2009)
│   ├── The Secret Life of Walter Mitty (2013)
│   ├── The.Secret.Of.NIMH.1982.720p.BluRay.x264-HALCYON
│   ├── The Signal (2014)
│   ├── The Social Network 720p
│   ├── The Sword in the Stone 1963 1080p BDRip H264 AAC - KiNGDOM
│   ├── The Thing 1982 1080p HDDVDRip H264 AAC - IceBane (Kingdom Release)
│   ├── The Thin Red Line 1998 Criterion Collection 720p BRRip x264-HDLiTE
│   ├── The Town 720p
│   ├── The.Usual.Suspects.1995.SLOSub.720p.BluRay.DTS.x264-ESiR
│   ├── The Warriors Director's Cut 1979 1080p BDRip H264 AAC - KiNGDOM
│   ├── The.Wind.Rises.2013.720p.BluRay.x264-PSYCHD
│   ├── The Witches 1990 720p HDTV x264
│   ├── The Worlds End 2013 720p BRRip x264 AC3-JYK
│   ├── Thor The Dark World (2013) [1080p]
│   ├── Time.Bandits.1981.REMASTERED.720p.BluRay.DTS.x264-PublicHD
│   ├── Titan.A.E.2000.720p.WEB-DL.DTS.H264-CtrlHD [PublicHD]
│   ├── To Have And Have Not
│   ├── True Grit
│   ├── Tyrannosaur 2011 LIMITED 1080p BRRip x264 AC3-26K
│   ├── United 93 720p MP4 AAC x264 BRRip 2006-CC
│   ├── Up in The Air
│   ├── Walk The Line 2005 Extended Cut 720p BRRip x264 Illidan91 (Kingdom-Release)
│   ├── Wolf Creek Unrated 2005 1080p HDDVDRip H264 AAC - KiNGDOM
│   └── 《用心棒》Yojimbo.1961.720p.BluRay.x264-SiNNERS-人人影视高清发布组
├── Movies
│   ├── 2 Guns (2013)
│   ├── Alan Partridge Alpha Papa (2013)
│   ├── Almost Famous EXTENDED (2000) [1080p]
│   ├── Anomalisa
│   ├── Arbitrage.2012.HDRiP.AC3-2.0.XviD-AXED
│   ├── Argo.2012.720p.BluRay.x264-SPARKS [PublicHD]
│   ├── Babel[2006]DvDrip[Eng]-aXXo
│   ├── Batman.Returns.1992.1080p.BluRay.x264-CiNEFiLE
│   ├── Batoru Rowaiaru (Battle Royale)[2000]DvDrip[JAP][ENG SUBS]-BugZ
│   ├── Brave.2012.R5.DVDRip.XViD.LiNE-UNiQUE
│   ├── CLAT18.SHULiBAN
│   ├── COLD FISH (2010) DVDRip (with subs) - wex0
│   ├── Concussion
│   ├── Dare Mo Shiranai aka Nobody Knows Sonata Premiere
│   ├── Deathgasm
│   ├── Departures (Okuribito 2008)
│   ├── Disconnect (2012) [1080p]
│   ├── Django.Unchained.2012.720p.BluRay.x264-SPARKS [PublicHD]
│   ├── Epic (2013)
│   ├── Fast.And.Furious.6.2013.1080p.WEB-DL.H264-BLUEBIRD [PublicHD]
│   ├── Film
│   ├── Funny Games U.S[2007]DvDrip[Eng]-FXG
│   ├── Gangster Squad (2013) [1080p]
│   ├── Identity Thief (2013)
│   ├── Inception.2010.1080p.BluRay.x264-REFiNED
│   ├── Indie.Game.The.Movie.2012.WEBRip.XviD-S4A
│   ├── Ip Man 3
│   ├── Iron Man 3
│   ├── Jack.the.Giant.Slayer.2013.BRRip.XviD-S4A
│   ├── Kick.Ass.2.2013.1080p
│   ├── Kung Fu Panda 3
│   ├── Lawless.2012.BDRip.XviD-SPARKS
│   ├── Les.Miserables.2012.720p.BluRay.x264-SPARKS [PublicHD]
│   ├── Life.of.Pi.2012.1080p.WEB-DL.H264-CrazyHD [PublicHD]
│   ├── Lincoln.2012.720p.BluRay.x264-SPARKS [publicHD]
│   ├── Love.And.Other.Drugs.2010.BrRip.Xvid {1337x}-Noir
│   ├── Love Exposure (2008)
│   ├── Machete Kills [2013] HDRip XViD-ETRG
│   ├── Magnolia (1999)
│   ├── Man of Steel (2013)
│   ├── Memories.of.Murder[Salinui.chueok].2003.BluRay.480p.H264
│   ├── Moon
│   ├── Mud (2012)
│   ├── Mulholland Dr (2001)
│   ├── New folder
│   ├── Ninja.Shadow.of.A.Tear.2013.HDRip.XviD-AQOS
│   ├── Now You See Me (2013)
│   ├── Oblivion (2013) [1080p]
│   ├── Old Boy_subbed
│   ├── Over The Edge[1979] Movie & Soundtrack
│   ├── Pain And Gain
│   ├── Paranormal.Activity.2.2010.UNRATED.DVDRip.XviD-Larceny
│   ├── People.Like.Us.2012.DVDRip.XviD-SPARKS
│   ├── Pirates.Of.The.Caribbean.Quadrilogy.1080p.BluRay.x264.anoXmous
│   ├── Prisoners [2013] HDRip XviD -ETRG
│   ├── Prometheus.2012.720p.WEB-DL.DD5.1.H.264-CtrlHD [PublicHD]
│   ├── Reservoir Dogs (1992) [1080p]
│   ├── Riddick (2013) DVDRip XviD-MAXSPEED
│   ├── Ruby.Sparks.2012.LIMITED.DVDRip.XviD-DEPRiVED
│   ├── Safety.Not.Guaranteed.2012.LIMITED.DVDRip.XviD-SPARKS
│   ├── Salmon.Fishing.In.The.Yemen.2011.BDRip.XviD-COCAIN
│   ├── Scary.Or.Die.2012.DVDRip.XviD-IGUANA
│   ├── Schindlers.List.1993.1080p.BluRay.x264-HD4U
│   ├── Seven.Psychopaths.2012.720p.BluRay.x264-SPARKS [PublicHD]
│   ├── Shame.2011.LIMITED.DVDRip.XviD-AMIABLE
│   ├── Shrek the Musical (2013) [1080p]
│   ├── SILVER LININGS DVDRIP EDAW2013
│   ├── Speak.2004.NTSC.DVD.x264-Tree
│   ├── Star Trek Into Darkness
│   ├── Star Wars Episode II Attack of the Clones (2002) [1080p]
│   ├── Star Wars Episode III Revenge of the Sith (2005) [1080p]
│   ├── Star Wars Episode I The Phantom Menace (1999) [1080p]
│   ├── Star Wars Episode IV A New Hope (1977) [1080p]
│   ├── Star Wars: Episode VII - The Force Awakens: The Story Awakens - The Table Read
│   ├── Star Wars Episode VI Return of the Jedi (1983) [1080p]
│   ├── Star Wars Episode V The Empire Strikes Back (1980) [1080p]
│   ├── Superbad Unrated (2007)
│   ├── Sweeney Todd (2007) [1080p]
│   ├── Talk To Her [Hable Con Ella].2002.DVDRip.XviD-VLiS
│   ├── The.Bling.Ring.2013.BRRip.XviD-S4A
│   ├── The Confirmation
│   ├── The Conjuring (2013)
│   ├── The Departed (2006) [1080p]
│   ├── The Family (2013)
│   ├── The Great Gatsby (2013)
│   ├── The Hobbit An Unexpected Journey (2012) [1080p]
│   ├── The Hours 2002 DvDrip XviD-ACME
│   ├── The Hunger Games: Mockingjay - Part 2
│   ├── The.Iceman.2012.BRRip XViD juggs
│   ├── The Internship (2013)
│   ├── The Kings of Summer (2013)
│   ├── The.Master.2012.720p.BluRay.DTS.x264-AXED [PublicHD]
│   ├── The Preppie Connection
│   ├── The Revenant
│   ├── There Will Be Blood (2007)
│   ├── The Sixth Sense [1999] DVDRip Xvid Blood
│   ├── This Is the End (2013)
│   ├── Titanic (1997)
│   ├── Warm Bodies (2013)
│   ├── Watchmen (2009)
│   ├── We're the Millers (2013)
│   ├── World.War.Z.2013.Unrated.Cut.720p.BluRay.x264.DTS-WiKi [PublicHD]
│   ├── [ www UsaBit com ] - Red 2 2013 DVDRip XviD-BiDA
│   ├── [ www.UsaBit.com ] - Ted.2012.WEBRip.XviD-RESiSTANCE
│   └── Zero.Dark.Thirty.2012.720p.BluRay.x264-Felony [PublicHD]
├── Movies_2
│   ├── Foxcatcher (2014) [1080p]
│   ├── Inside.Out.2015.720p.WEBRip.x264.AAC2.0-RARBG
│   ├── Kingsman.The.Secret.Service.2014.720p.WEB-DL.XviD.AC3-RARBG
│   ├── Kurt Cobain Montage of Heck (2015) [1080p]
│   ├── Louis.CK.Live.At.The.Comedy.Store.2015.720p.WEBRip.XviD.MP3-RARBG
│   └── Mad.Max.Fury.Road.2015.1080p.WEB-DL.DD5.1.H264-RARBG
├── Movies 2015
│   ├── Ant-Man.2015.1080p.WEBRip.x264.AAC2.0-RARBG
│   ├── Bone.Tomahawk.2015.720p.WEB-DL.DD5.1.H264-RARBG
│   ├── Bridge.of.Spies.2015.1080p.BluRay.H264.AAC-RARBG
│   ├── Brooklyn.2015.1080p.BluRay.H264.AAC-RARBG
│   ├── Carol.2015.1080p.BluRay.H264.AAC-RARBG
│   ├── Ex.Machina.2015.1080p.BluRay.x264-SPARKS[rarbg]
│   ├── In.the.Heart.of.the.Sea.2015.1080p.BluRay.H264.AAC-RARBG
│   ├── Krampus.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── Mission.Impossible.Rogue.Nation.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── No.Escape.2015.720p.BluRay.H264.AAC-RARBG
│   ├── Room.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── Shaun.the.Sheep.The.Movie.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── Sicario 2015 720p BDRip x264 AC3-Mikas
│   ├── Spotlight.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── Steve.Jobs.2015.1080p.BluRay.H264.AAC-RARBG
│   ├── Straight.Outta.Compton.2015.DC.1080p.BluRay.H264.AAC-RARBG
│   ├── Ted 2 2015 1080p WEB-DL x264 AC3-JYK
│   ├── The.Big.Short.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── The.Dressmaker.2015.1080p.BluRay.H264.AAC-RARBG
│   ├── The.Girl.In.the.Book.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── The.Good.Dinosaur.2015.1080p.BluRay.x264-SPARKS[rarbg]
│   ├── The.Intern.2015.720p.WEBRip.x264.AAC2.0-FGT
│   ├── The.Lobster.2015.720p.WEB-DL.DD5.1.H264-FGT
│   ├── The.Man.from.U.N.C.L.E.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── The.Martian.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── The.Night.Before.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── The.Peanuts.Movie.2015.720p.BluRay.x264-DRONES[rarbg]
│   ├── The SpongeBob Movie
│   └── Trumbo.2015.1080p.BluRay.H264.AAC-RARBG
├── Movies 2016
│   ├── Air 2015 720p WEB-DL DD5 1 H264-RARBG
│   ├── Air.2015.720p.WEB-DL.DD5.1.H264-RARBG
│   ├── Avengers.Age.of.Ultron.2015.720p.WEB-DL.DD5.1.H264-RARBG
│   ├── Birdman.2014.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── Chappie.2015.1080p.WEB-DL.AAC2.0.H264-RARBG
│   ├── Citizenfour (2014) [1080p]
│   ├── Cop Car 2015 720p WEB-DL DD5 1 H264-RARBG
│   ├── Dark Places 2015 720p WEB-DL DD5 1 H264-RARBG
│   ├── Finding Dory
│   ├── Fury.2014.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── Jurassic.World.2015.1080p.WEB-DL.AAC2.0.H264-RARBG
│   ├── Kubo and the Two Strings
│   ├── Mad.Max.Fury.Road.2015.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── Nightcrawler.2014.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── Pete's Dragon
│   ├── Sherlock.The.Abominable.Bride.2016.1080p.WEB-DL.DD5.1.H264-Coo7[rarbg]
│   ├── The BFG
│   ├── The.Hateful.Eight.2015.720p.BluRay.x264-SPARKS[rarbg]
│   └── Whiplash.2014.720p.WEB-DL.AAC2.0.H264-RARBG
├── Movies_3
│   ├── 12.Years.A.Slave.2013.1080p.WEB-DL.H264-PublicHD
│   ├── A.Dangerous.Method.2011.LIMITED.1080p.BluRay.H264.AAC-RARBG
│   ├── A.Girl.Walks.Home.Alone.at.Night.2014.PERSIAN.720p.WEB-DL.DD5.1.H264-FGT
│   ├── Ain't Them Bodies Saints (2013) [1080p]
│   ├── All.Is.Lost.2013.720p.WEB-DL.H264-PublicHD
│   ├── American Hustle 2013 BRRip 720p x264 AAC - KiNGDOM
│   ├── A.Most.Violent.Year.2014.1080p.WEB-DL.DD5.1.H264-RARBG
│   ├── August Osage County (2013)
│   ├── BBC Addicted to Pleasure
│   ├── Blue.Jasmine.2013.1080p.WEB-DL.H264-PublicHD
│   ├── Captain Phillips 2013 720p BRRip x264 AC3-JYK
│   ├── Dallas Buyers Club (2013) [1080p]
│   ├── Dawn of the Planet of the Apes (2014)
│   ├── Fading Gigolo (2013) [1080p]
│   ├── Frontera.2014.720p.WEB-DL.x264[ETRG]
│   ├── Ghost World 2001 HDTV XvidHD 720p-NPW
│   ├── Hot.Shots.1991.XviD-BGR
│   ├── Interstellar.2014.IMAX.1080p.Bluray.x264.DTS-EVO
│   ├── Into the Wild (2007) [1080p]
│   ├── Just.Before.I.Go.2014.1080p.WEB-DL.DD5.1.H.264-RARBG
│   ├── [Kametsu] Grave of the Fireflies - [Blu-Ray][690p][0388C75B]
│   ├── Last Action Hero [1993] 1080p BluRay AAC x264-tomcat12[ETRG]
│   ├── Locke (2013) [1080p]
│   ├── Stephen.Hawkings.Grand.Design.2012.720p.BluRay.x264-WaLMaRT [PublicHD]
│   ├── The Double (2013)
│   ├── The.Godfather.Trilogy.[ I. II. III ].1080p.BluRay.x264.anoXmous
│   ├── The_Past_2013_720p__TinyMoviez
│   ├── The Past (2013).srt
│   ├── The.Past.720p & 1080p - Iman-SI.srt
│   ├── Wild.2014.720p.BluRay.x264-SPARKS[rarbg]
│   └── You Dont Mess with the Zohan (2008) [1080p]
├── Movies_4
│   ├── 12.Years.A.Slave.2013.1080p.WEB-DL.H264-PublicHD
│   ├── 22 Jump Street (2014) WEBDL DVDRip XviD-MAXSPEED
│   ├── Ain't Them Bodies Saints (2013) [1080p]
│   ├── All.Is.Lost.2013.720p.WEB-DL.H264-PublicHD
│   ├── American Hustle 2013 BRRip 720p x264 AAC - KiNGDOM
│   ├── Anchorman.2.The.Legend.Continues.2013.UNRATED.1080p.WEB-DL.H264-PublicHD
│   ├── August Osage County (2013)
│   ├── Blue.Is.the.Warmest.Color.2013.720p.BluRay.x264-PSYCHD [PublicHD]
│   ├── Blue.Jasmine.2013.1080p.WEB-DL.H264-PublicHD
│   ├── Boyhood (2014)
│   ├── Captain Phillips 2013 720p BRRip x264 AC3-JYK
│   ├── Dallas Buyers Club (2013) [1080p]
│   ├── Ed Wood (1994) [1080p]
│   ├── Gone Girl (2014) WEBDL DVDRip XviD-MAXSPEED
│   ├── Gravity.2013.1080p.WEB-DL.H264-PublicHD
│   ├── Gravity.3D.2013.1080p.BluRay.Half-SBS.DTS.x264-PublicHD
│   ├── Inside.Llewyn.Davis.2013.720p.BluRay.x264-ALLiANCE [PublicHD]
│   ├── Maleficent (2014)
│   ├── Nebraska (2013) 1080p x264 DD5.1
│   ├── Philomena.2013.720p.WEB-DL.H264-PublicHD
│   ├── Prisoners.2013.720p.WEB-DL.H264-PublicHD
│   ├── Rush (2013) [1080p]
│   ├── Saving Mr. Banks (2013)
│   ├── The Giver (2014)
│   ├── The Grandmaster 2013 720p BRRip x264 AC3-JYK
│   ├── The.Great.Beauty.2013
│   ├── The.Hobbit.The.Desolation.Of.Smaug.2013.720p.BluRay.DTS.x264-PublicHD
│   ├── The.Hunt.2012.720p.BluRay.DTS.x264-HDWinG [PublicHD]
│   └── The.Wolverine.2013.EXTENDED.720p.BluRay.x264-SPARKS
├── Movies Mori
│   ├── 13.Assassins.2010.720p.BDRip.XviD.AC3-ViSiON
│   ├── 48.Hrs.1982.1080p.BluRay.x264-TENEIGHTY
│   ├── Alien.1979.1080p.MKV.x264.AC3.DTS.Eng.NLSubs-DMT
│   ├── Alien.3.1992.Special.Edition.1080p.BluRay.H264.AAC-RARBG
│   ├── Aliens (1986) 1080p MKV x264 AC3+DTS NLSubs DMT
│   ├── Apollo.13.1995.BluRay.720p.DTS.2Audio.x264-CHD
│   ├── A.Serious.Man.2009.LIMITED.1080p.BluRay.x264
│   ├── Attack.The.Block.2011.720p.BluRay.x264-iNFAMOUS
│   ├── Audition.1999.720p.BluRay.x264-CiNEFiLE
│   ├── Bernie (2011) 1080p x264 DD5.1 Eng NL Subs
│   ├── Big Trouble in Little China 720p
│   ├── Blade.Runner.Final.Cut.1997.720p.BluRay.x264-WiKi
│   ├── Boogie.Nights.1997.PROPER.720p.BluRay.x264-ROLLERGiRL
│   ├── Bronson 2008 LIMITED BRRip 720p x264 AAC - KiNGDOM
│   ├── Close Encounters Of The Third Kind 1977 1080p BDRip H264 AAC - IceBane (Kingdom Release)
│   ├── Cold.in.July.2014.720p.BluRay.x264.DTS-RARBG
│   ├── Crazy.Stupid.Love.2011.720p.BRRip.XviD.AC3-ViSiON
│   ├── Dark.City.1998.Directors.Cut.BluRay.1080p.x264.DTS-LTT
│   ├── District 9 720p
│   ├── Dreamcatcher.2003.720p.WEB-DL.H264-ViGi [PublicHD]
│   ├── Elysium.2013.720p.BluRay.DTS.x264-DNL
│   ├── Enemy.2013.1080p.WEB-DL.H264-PublicHD
│   ├── Falling Down-720p MP4 AAC x264 BRRip 1993-CC
│   ├── Get.the.Gringo.2012.BRRIP.720P.H264-ZEKTORM
│   ├── Ghost.Dog.The.Way.Of.The.Samurai.1999.720p.BluRay.x264-LCHD
│   ├── Good Morning Vietnam 1987 1080p BDRip H264 AAC - KiNGDOM
│   ├── Gremlins.1984.720p.BRRip.XviD.AC3-ViSiON
│   ├── Haywire.2011.720p.BluRay.X264-BLOW
│   ├── Heavy.Metal.1981.720p.HDTV.x264-aAF
│   ├── I Love You Phillip Morris
│   ├── Killer.Joe.2011.720p.BluRay.x264-DESPiTE [PublicHD]
│   ├── Kill.List.2011.720p.BluRay.X264-7SinS
│   ├── Limitless Unrated 2011 BRRip 1080p x264 AAC - honchorella (Kingdom Release)
│   ├── Natural.Born.Killers.1994.m-HD.x264-LDK
│   ├── Near.Dark.1987.720p.Bluray.x264-hV
│   ├── Oblivion 2013 1080p BDRip H264 AAC - KiNGDOM
│   ├── Outrage.2010.BlyRay.720p.DTS.x264-CHD
│   ├── Reservoir Dogs 720p
│   ├── Risky.Business.1983.720p.BluRay.DTS.x264-iLL
│   ├── Scott.Pilgrim.Vs.The.World.2010.720p.BRRip.XviD.AC3-ViSiON
│   ├── Source.Code.2011.720p.BRRip.x264.AAC-ViSiON
│   ├── Sparrow.2008.m-HD.x264-LKD
│   ├── The A-Team Extended Ed. 2010 1080p BRRip H264 AAC - IceBane (Kingdom Release)
│   ├── The Crow
│   ├── The Devil's Double (2011) x264 1080p DTS & DD 5.1 NL Subs DMT
│   ├── The.Guard.720p.Bluray.x264-iNFAMOUS
│   ├── The.Guest.2014.1080p.BRRip.x264.AC3-RARBG
│   ├── The Imitation Game 2014 1080p BRRip x264 DTS-JYK
│   ├── The Purge Anarchy 2014 720p BRRip x264 AAC-KiNGDOM
│   └── The Town 720p
├── Movies Random
│   ├── 2001: A Space Odyssey
│   ├── Arizona Dream
│   ├── Being John Malkovich
│   ├── Cast Away
│   ├── Citizen Kane
│   ├── Close Encounters of the Third Kind
│   ├── Dirty Pictures
│   ├── Inner Worlds, Outer Worlds
│   ├── Into the Wild
│   ├── La Dolce Vita
│   ├── La La Land
│   ├── Little Miss Sunshine
│   ├── Louis.C.K.2017.2017.720p.WEBRip.x264-RARBG
│   ├── Magic Trip: Ken Kesey's Search for a Kool Place
│   ├── Shame
│   ├── Split
│   ├── The 68th Annual Primetime Emmy Awards 2016 720p HDTV x264-ALTEREGO
│   ├── The Intouchables
│   └── The Substance: Albert Hofmann's LSD
└── Woody Allens
    ├── Alice (1990) Woody Allen
    ├── Annie.Hall.1977.1080p.BluRay.H264.AAC-RARBG
    ├── Another Woman 1988 720p HDRip x264 titler
    ├── Anything.Else.2003.720p.BluRay.H264.AAC-RARBG
    ├── Broadway Danny Rose 1984 1080p BluRay H264 AAC-RARBG
    ├── Bullets.Over.Broadway.1994.1080p.BluRay.H264.AAC-RARBG
    ├── Crimes.and.Misdemeanors.1989.1080p.BluRay.H264.AAC-RARBG
    ├── Deconstructing Harry (1997) 720p WEB-DL x264 650MB (Ganool)-XpoZ
    ├── Everyone.Says.I.Love.You.1996.720p.BluRay.H264.AAC-RARBG
    ├── Everything.You.Always.Wanted.to.Know.About.Sex.But.Were.Afraid.to.Ask.1972.720p.BluRay.H264.AAC-RARBG
    ├── Hannah.and.Her.Sisters.1986.720p.BluRay.H264.AAC-RARBG
    ├── Hollywood.Ending.2002.720p.BluRay.H264.AAC-RARBG
    ├── Husbands.and.Wives.1992.720p.WEB-DL.AAC2.0.h264-HAi
    ├── Interiors.1978.1080p.BluRay.H264.AAC-RARBG
    ├── Love.and.Death.1975.720p.BluRay.H264.AAC-RARBG
    ├── Manhattan.1979.1080p.BluRay.H264.AAC-RARBG
    ├── Manhattan.Murder.Mystery.1993.720p.WEB-DL.AAC2.0.h264-HAi
    ├── Mighty.Aphrodite.1995.1080p.BluRay.H264.AAC-RARBG
    ├── Radio.Days.1987.1080p.BluRay.H264.AAC-RARBG
    ├── September.1987.720p.WEB.x264-REGRET[PRiME]
    ├── Sleeper.1973.720p.BluRay.x264-Japhson [PublicHD]
    ├── Stardust.Memories.1980.720p.BluRay.H264.AAC-RARBG
    ├── The.Curse.of.the.Jade.Scorpion.2001.720p.BluRay.H264.AAC-RARBG
    ├── The.Purple.Rose.of.Cairo.1985.720p.BluRay.H264.AAC-RARBG
    └── Zelig.1983.1080p.BluRay.H264.AAC-RARBG

548 directories, 2 files
```

### After :
```
.
├── 1915
│   └── The Curse of the Black Pearl
├── 1939
│   └── Goodbye, Mr. Chips
├── 1941
│   └── Citizen Kane
├── 1944
│   └── To Have and Have Not
├── 1954
│   ├── On the Waterfront
│   └── Seven Samurai
├── 1956
│   └── Hot Shots
├── 1957
│   └── Wild Strawberries
├── 1960
│   └── La Dolce Vita
├── 1961
│   └── Yojimbo
├── 1962
│   └── Lawrence of Arabia
├── 1963
│   └── The Sword in the Stone
├── 1965
│   ├── Dead Man's Chest
│   └── Film
├── 1966
│   └── The Good, the Bad and the Ugly
├── 1967
│   ├── Birdman
│   └── Guess Who's Coming to Dinner
├── 1968
│   ├── 2001: A Space Odyssey
│   ├── Charly
│   └── The City of Gods
├── 1969
│   └── Bob & Carol & Ted & Alice
├── 1971
│   └── The Boy Friend
├── 1972
│   └── Everything You Always Wanted to Know About Sex * But Were Afraid to Ask
├── 1973
│   └── Sleeper
├── 1975
│   ├── Love and Death
│   └── Monty Python and the Holy Grail
├── 1977
│   ├── Annie Hall
│   ├── Close Encounters of the Third Kind
│   └── Star Wars: Episode IV - A New Hope
├── 1978
│   ├── Interiors
│   └── Les Miserables
├── 1979
│   ├── Apocalypse Now
│   ├── Life of Brian
│   ├── Manhattan
│   ├── Over the Edge
│   └── The Warriors
├── 1980
│   ├── Stardust Memories
│   └── Star Wars: Episode V - The Empire Strikes Back
├── 1981
│   ├── Heavy Metal
│   └── Time Bandits
├── 1982
│   ├── 48 Hrs.
│   ├── Blade Runner
│   ├── The Red Line
│   ├── The Secret of NIMH
│   └── The Thing
├── 1983
│   ├── Risky Business
│   ├── Star Wars: Episode VI - Return of the Jedi
│   ├── The Meaning of Life
│   ├── The Right Stuff
│   └── Zelig
├── 1984
│   ├── Broadway Danny Rose
│   ├── Conan the Destroyer
│   └── Gremlins
├── 1985
│   ├── Back to the Future
│   └── The Purple Rose of Cairo
├── 1986
│   ├── A Better Tomorrow
│   ├── Big Trouble in Little China
│   └── Hannah and Her Sisters
├── 1987
│   ├── Good Morning, Vietnam
│   ├── Near Dark
│   ├── Radio Days
│   └── September
├── 1988
│   ├── Another Woman
│   ├── Die Hard
│   └── Grave of the Fireflies
├── 1989
│   ├── Crimes and Misdemeanors
│   └── Santa Sangre
├── 1990
│   ├── Alice
│   ├── Goodfellas
│   ├── Hardware
│   ├── Mulberry Street
│   └── The Witches
├── 1991
│   └── City Slickers
├── 1992
│   ├── Alien 3
│   ├── Batman Returns
│   ├── Husbands and Wives
│   └── Reservoir Dogs
├── 1993
│   ├── Arizona Dream
│   ├── Cronos
│   ├── Falling Down
│   ├── Last Action Hero
│   ├── Manhattan Murder Mystery
│   └── Schindler's List
├── 1994
│   ├── Bullets Over Broadway
│   ├── Ed Wood
│   ├── In the Mouth of Madness
│   ├── Little Women
│   ├── Natural Born Killers
│   ├── Pulp Fiction
│   └── The Crow
├── 1995
│   ├── Apollo 13
│   ├── Mighty Aphrodite
│   └── The Usual Suspects
├── 1996
│   └── Everyone Says I Love You
├── 1997
│   ├── Boogie Nights
│   ├── Deconstructing Harry
│   ├── L.A. Confidential
│   ├── Liar Liar
│   ├── Princess Mononoke
│   └── Titanic
├── 1998
│   ├── Dark City
│   ├── Fear and Loathing in Las Vegas
│   ├── Ronin
│   └── Small Soldiers
├── 1999
│   ├── Audition
│   ├── Being John Malkovich
│   ├── Ghost Dog: The Way of the Samurai
│   ├── Mulholland Dr.
│   ├── Star Wars: Episode I - The Phantom Menace
│   └── The Sixth Sense
├── 2000
│   ├── Almost Famous
│   ├── Cast Away
│   ├── Dirty Pictures
│   ├── Me, Myself & Irene
│   ├── O Brother, Where Art Thou?
│   ├── Snatch
│   └── Titan A.E.
├── 2001
│   ├── Ghost World
│   ├── Spirited Away
│   ├── The Curse of the Jade Scorpion
│   └── The Devil's Backbone
├── 2002
│   ├── Hollywood Ending
│   ├── Road to Perdition
│   ├── Star Wars: Episode II - Attack of the Clones
│   ├── Talk to Her
│   ├── The Bourne Identity
│   └── The Hours
├── 2003
│   ├── Anything Else
│   ├── Dreamcatcher
│   ├── Finding Nemo
│   ├── Master and Commander: The Far Side of the World
│   ├── Memories of Murder
│   └── Mystic River
├── 2004
│   ├── Anchorman: The Legend of Ron Burgundy
│   ├── Eternal Sunshine of the Spotless Mind
│   ├── Million Dollar Baby
│   ├── Nobody Knows
│   ├── Pachinko batoru rowaiaru II
│   ├── Speak
│   ├── The Bourne Supremacy
│   ├── The Chronicles of Riddick
│   └── The Machinist
├── 2005
│   ├── Batman Begins
│   ├── King Kong
│   ├── Madagascar
│   ├── Match Point
│   ├── Star Wars: Episode III - Revenge of the Sith
│   ├── Walk the Line
│   └── Wolf Creek
├── 2006
│   ├── Babel
│   ├── Borat: Cultural Learnings of America for Make Benefit Glorious Nation of Kazakhstan
│   ├── Children of Men
│   ├── Little Miss Sunshine
│   ├── Sweeney Todd
│   ├── The Departed
│   ├── The Lord of the Rings Trilogy: Behind-the-Scenes
│   └── United 93
├── 2007
│   ├── Before the Devil Knows You're Dead
│   ├── Funny Games
│   ├── Into the Wild
│   ├── Rendition
│   ├── Superbad
│   ├── The Bourne Ultimatum
│   └── There Will Be Blood
├── 2008
│   ├── Bronson
│   ├── Departures
│   ├── In Bruges
│   ├── Love Exposure
│   ├── Madagascar: Escape 2 Africa
│   ├── Pineapple Express
│   ├── Sparrow
│   ├── The Good the Bad the Weird
│   ├── The Hurt Locker
│   └── You Don't Mess with the Zohan
├── 2009
│   ├── About Elly
│   ├── A Serious Man
│   ├── At World's End
│   ├── Avatar
│   ├── District 9
│   ├── I Love You Phillip Morris
│   ├── Inglourious Basterds
│   ├── Julie & Julia
│   ├── Moon
│   ├── Polytechnique
│   ├── Sherlock Holmes
│   ├── Solomon Kane
│   ├── Star Trek
│   ├── The Road
│   └── Up in the Air
├── 2010
│   ├── 13 Assassins
│   ├── Alice in Wonderland
│   ├── Blue Valentine
│   ├── Cold Fish
│   ├── Don't Be Afraid of the Dark
│   ├── Incendies
│   ├── Inception
│   ├── Jackass 3D
│   ├── Love & Other Drugs
│   ├── Nikita
│   ├── Outrage
│   ├── Paranormal Activity 2
│   ├── Scott Pilgrim vs. the World
│   ├── Shutter Island
│   ├── The A-Team
│   ├── The Fighter
│   ├── The Ghost Writer
│   ├── The King's Speech
│   ├── The Next Three Days
│   ├── The Other Guys
│   ├── The Social Network
│   ├── The Town
│   └── True Grit
├── 2011
│   ├── A Better Tomorrow 2
│   ├── A Dangerous Method
│   ├── A Separation
│   ├── Attack the Block
│   ├── Bernie
│   ├── Cars 2
│   ├── Contagion
│   ├── Crazy, Stupid, Love.
│   ├── Green Lantern
│   ├── Haywire
│   ├── Hugo
│   ├── J. Edgar
│   ├── Killer Joe
│   ├── Kill List
│   ├── Kung Fu Panda 2
│   ├── Limitless
│   ├── Magic Trip: Ken Kesey's Search for a Kool Place
│   ├── Midnight in Paris
│   ├── Mission: Impossible - Ghost Protocol
│   ├── Moneyball
│   ├── My Week with Marilyn
│   ├── Pirates of the Caribbean: On Stranger Tides
│   ├── Pirates of the Caribbean: On Stranger Tides 35mm 3D Special
│   ├── Rampart
│   ├── Real Steel
│   ├── Salmon Fishing in the Yemen
│   ├── Shame
│   ├── Sherlock Holmes: A Game of Shadows
│   ├── Take Shelter
│   ├── The Adventures of Tintin
│   ├── The Descendants
│   ├── The Devil's Double
│   ├── The Girl with the Dragon Tattoo
│   ├── The Guard
│   ├── The Hangover Part II
│   ├── The Help
│   ├── The Ides of March
│   ├── The Intouchables
│   ├── The Muppets
│   ├── The Rum Diary
│   ├── The Substance: Albert Hofmann's LSD
│   ├── The Tree of Life
│   ├── The Turin Horse
│   ├── Tinker Tailor Soldier Spy
│   ├── Tower Heist
│   ├── Tyrannosaur
│   ├── War Horse
│   ├── Warrior
│   └── X-Men First Class Rejects
├── 2012
│   ├── 21 Jump Street
│   ├── Addicted to Pleasure
│   ├── Arbitrage
│   ├── Argo
│   ├── Brave
│   ├── Chronicle
│   ├── Cloud Atlas
│   ├── Dark Shadows
│   ├── Disconnect
│   ├── Django Unchained
│   ├── End of Watch
│   ├── Frankenweenie
│   ├── Get the Gringo
│   ├── Indie Game: The Movie
│   ├── Inner Worlds, Outer Worlds
│   ├── John Carter
│   ├── Lawless
│   ├── Life of Pi
│   ├── Lincoln
│   ├── Lockout
│   ├── Looper
│   ├── Magic Mike
│   ├── Men in Black 3
│   ├── Moonrise Kingdom
│   ├── Mud
│   ├── ParaNorman
│   ├── People Like Us
│   ├── Project X
│   ├── Prometheus
│   ├── Ruby Sparks
│   ├── Safe House
│   ├── Scary or Die
│   ├── Seven Psychopaths
│   ├── Silver Linings Playbook
│   ├── Skyfall
│   ├── Snow White and the Huntsman
│   ├── Stephen Hawking's Grand Design
│   ├── The 84th Annual Academy Awards
│   ├── The Avengers
│   ├── The Cabin in the Woods
│   ├── The Dark Knight Rises
│   ├── The Dictator
│   ├── The Expendables 2
│   ├── The Hobbit: An Unexpected Journey
│   ├── The Hunger Games
│   ├── The Hunt
│   ├── The Iceman
│   ├── The Lorax
│   ├── The Master
│   ├── Wrath of the Titans
│   └── Zero Dark Thirty
├── 2013
│   ├── 12 Years a Slave
│   ├── 2 Guns
│   ├── Afflicted
│   ├── Ain't Them Bodies Saints
│   ├── Alan Partridge
│   ├── All Is Lost
│   ├── American Hustle
│   ├── Anchorman 2: The Legend Continues
│   ├── August: Osage County
│   ├── Bad Grandpa
│   ├── Behind the Candelabra
│   ├── Blue Is the Warmest Color
│   ├── Blue Jasmine
│   ├── Captain Phillips
│   ├── Cloudy with a Chance of Meatballs 2
│   ├── Dallas Buyers Club
│   ├── Elysium
│   ├── Ender's Game
│   ├── Epic
│   ├── Escape Plan
│   ├── Evil Dead
│   ├── Fading Gigolo
│   ├── Fast & Furious 6
│   ├── Frozen
│   ├── Gangster Squad
│   ├── Gravity
│   ├── Identity Thief
│   ├── Inside Llewyn Davis
│   ├── Iron Man 3
│   ├── Jack the Giant Slayer
│   ├── Joe
│   ├── Kick-Ass 2
│   ├── Kill Your Darlings
│   ├── Locke
│   ├── Lone Survivor
│   ├── Machete Kills
│   ├── Man of Steel
│   ├── Nebraska
│   ├── Ninja: Shadow of a Tear
│   ├── Now You See Me
│   ├── Oblivion
│   ├── Oculus
│   ├── Old Boy
│   ├── Only Lovers Left Alive
│   ├── Out of the Furnace
│   ├── Pain & Gain
│   ├── Philomena
│   ├── Prisoners
│   ├── Riddick
│   ├── Rush
│   ├── Saving Mr. Banks
│   ├── Shrek the Musical
│   ├── Side Effects
│   ├── Star Trek Into Darkness
│   ├── The Bling Ring
│   ├── The Conjuring
│   ├── The Double
│   ├── The Family
│   ├── The Fifth Estate
│   ├── The Grandmaster
│   ├── The Great Beauty
│   ├── The Great Gatsby
│   ├── The Hobbit: The Desolation of Smaug
│   ├── The Internship
│   ├── The Kings of Summer
│   ├── The Past
│   ├── The Red 2 Experience
│   ├── The Secret Life of Walter Mitty
│   ├── The Wind Rises
│   ├── The Wolverine
│   ├── The World's End
│   ├── This Is the End
│   ├── Thor: The Dark World
│   ├── Warm Bodies
│   ├── We're the Millers
│   └── World War Z
├── 2014
│   ├── 22 Jump Street
│   ├── 300: Rise of an Empire
│   ├── A Girl Walks Home Alone at Night
│   ├── A Most Violent Year
│   ├── Boyhood
│   ├── Citizenfour
│   ├── Cold in July
│   ├── Dawn of the Planet of the Apes
│   ├── Ex Machina
│   ├── Foxcatcher
│   ├── Frontera
│   ├── Fury
│   ├── Gone Girl
│   ├── Interstellar
│   ├── Just Before I Go
│   ├── Kingsman: The Secret Service
│   ├── Maleficent
│   ├── Nightcrawler
│   ├── Non-Stop
│   ├── The Amazing Spider-Man 2
│   ├── The Giver
│   ├── The Guest
│   ├── The Imitation Game
│   ├── The Interview
│   ├── The Lego Movie
│   ├── The Monuments Men
│   ├── The Purge: Anarchy
│   ├── The Signal
│   ├── Whiplash
│   └── Wild
├── 2015
│   ├── Air
│   ├── Anomalisa
│   ├── Ant-Man
│   ├── Avengers: Age of Ultron
│   ├── Bone Tomahawk
│   ├── Bridge of Spies
│   ├── Brooklyn
│   ├── Carol
│   ├── Chappie
│   ├── Cobain: Montage of Heck
│   ├── Concussion
│   ├── Cop Car
│   ├── Dark Places
│   ├── Deathgasm
│   ├── Exorcist
│   ├── Hitchcock Truffaut
│   ├── Inside Out
│   ├── In the Heart of the Sea
│   ├── Ip Man 3
│   ├── Jurassic World
│   ├── Krampus
│   ├── Louis C.K.: Live at the Comedy Store
│   ├── Mad Max: Fury Road
│   ├── Mission: Impossible - Rogue Nation
│   ├── No Escape
│   ├── Room
│   ├── Shaun the Sheep the Movie Green Light to Opening Night
│   ├── Sicario
│   ├── Spotlight
│   ├── Steve Jobs
│   ├── Straight Outta Compton
│   ├── Ted 2
│   ├── The Big Short
│   ├── The Dressmaker
│   ├── The Girl in the Book
│   ├── The Good Dinosaur
│   ├── The Hateful Eight
│   ├── The Intern
│   ├── The Lobster
│   ├── The Man from U.N.C.L.E.
│   ├── The Martian
│   ├── The Night Before
│   ├── The Peanuts Movie
│   ├── The Preppie Connection
│   ├── The Revenant
│   ├── The SpongeBob Movie: Sponge Out of Water
│   └── Trumbo
├── 2016
│   ├── Captain America: Civil War
│   ├── Finding Dory
│   ├── Kubo and the Two Strings
│   ├── Kung Fu Panda 3
│   ├── La La Land
│   ├── Life+1Day
│   ├── Lion
│   ├── Pawns No More: Making the Hunger Games: Mockingjay Part 2
│   ├── Pete's Dragon
│   ├── Split
│   ├── Star Wars: Episode VII - The Force Awakens: The Story Awakens - The Table Read
│   ├── The 68th Annual Primetime Emmy Awards 2016 720p HDTV x264-ALTEREGO
│   ├── The BFG
│   ├── The Confirmation
│   └── The Counselor
└── 2017
│   └── Louis C.K. 2017
└── Directors
        ├── Adam McKay
        ├── Akira Kurosawa
        ├── Alejandro Gonzalez Inarritu
        ├── Alexander Payne
        ├── Alfred Hitchcock
        ├── Andrew Stanton
        ├── Asghar Farhadi
        ├── Bryan Singer
        ├── Christopher Miller
        ├── Christopher Nolan
        ├── Clint Eastwood
        ├── Danny Boyle
        ├── Darren Aronofsky
        ├── David Fincher
        ├── David Lynch
        ├── David O. Russell
        ├── Denis Villeneuve
        ├── Ethan Coen
        ├── Federico Fellini
        ├── Francis Ford Coppola
        ├── George Lucas
        ├── Guillermo del Toro
        ├── Guy Ritchie
        ├── Hayao Miyazaki
        ├── Isao Takahata
        ├── James Cameron
        ├── Jeff Nichols
        ├── Jim Jarmusch
        ├── Joel Coen
        ├── John Carney
        ├── John Carpenter
        ├── Kar-Wai Wong
        ├── Kathryn Bigelow
        ├── Krzysztof Kieslowski
        ├── Lars von Trier
        ├── Martin Scorsese
        ├── Neill Blomkamp
        ├── Oliver Stone
        ├── Paul Greengrass
        ├── Paul Thomas Anderson
        ├── Peter Jackson
        ├── Phil Lord
        ├── Quentin Tarantino
        ├── Richard Linklater
        ├── Ridley Scott
        ├── Robert Zemeckis
        ├── Roman Polanski
        ├── Ron Howard
        ├── Sam Mendes
        ├── Sidney Lumet
        ├── Stanley Kubrick
        ├── Steven Soderbergh
        ├── Steven Spielberg
        ├── Terrence Malick
        ├── Terry Gilliam
        ├── Terry Jones
        ├── Tim Burton
        └── Woody Allen

542 directories, 0 files
```
