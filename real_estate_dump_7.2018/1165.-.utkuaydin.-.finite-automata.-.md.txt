# Regular Expression Engine

Final project for Formal Languages and Automata Theory (CMP3004) course, by Utku Aydın and Ömer Buğra Selvi.

## Design and Implementation

In `main.cpp`, the program reads two arguments: the filename and the regular expression. Then `Engine::createNFA()` first
converts the given expression to a postfix expression and then constructs a NFA by parsing it. After the NFA is constructed
then the program reads every line in the input file and checks if the any string sequence that's accepted by the NFA exists
in the line.

### NFA construction

Construction of NFA is done by using a stack. After reading each character of the postfix expression, a new NFA is created
by simply running NFA class' relevant operation method.

### Regular expression evaluation

`NFA::accepts()` method returns true whenver given string has a substring that adheres to the given regular expression. The
algorithm starts by finding which states which we can transition into from the inital state. First, it finds epsilon
transitions, then it finds all states we can transition into by using the currently evaluated character. If all goes well,
and we arrive into any final state, `NFA::accepts()` returns true.

### Tests

We used Fyodor Dostoevsky's Crime and Punishment, The Brothers Karamazov and The Idiot books for testing our program. Results
can be found at sample outputs section.

## Execution

```
RegexEngine <expression> <filename>
```

## Sample Outputs
```
$ ./RegexEngine Inquisitor samples/the_brothers_karamazov.txt
The following NFA was built:
Initial State: 
0
All States: 
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
Accepted States: 
[19]
Transitions: 
(0, 1, 'I')
(2, 3, 'n')
(1, 2, epsilon)
(4, 5, 'q')
(3, 4, epsilon)
(6, 7, 'u')
(5, 6, epsilon)
(8, 9, 'i')
(7, 8, epsilon)
(10, 11, 's')
(9, 10, epsilon)
(12, 13, 'i')
(11, 12, epsilon)
(14, 15, 't')
(13, 14, epsilon)
(16, 17, 'o')
(15, 16, epsilon)
(18, 19, 'r')
(17, 18, epsilon)
Accepted, line 94:       Chapter V. The Grand Inquisitor
Accepted, line 11045: “My poem is called ‘The Grand Inquisitor’; it’s a ridiculous thing, but I
Accepted, line 11050: Chapter V. The Grand Inquisitor
Accepted, line 11143: Dei_, been burnt by the cardinal, the Grand Inquisitor, in a magnificent
Accepted, line 11176: cardinal himself, the Grand Inquisitor, passes by the cathedral. He is an
Accepted, line 11191: Inquisitor. He blesses the people in silence and passes on. The guards
Accepted, line 11196: the prison is suddenly opened and the Grand Inquisitor himself comes in
Accepted, line 11637: it’s false—those are the worst of the Catholics, the Inquisitors, the
Accepted, line 11639: Inquisitor. What are these sins of mankind they take on themselves? Who
Accepted, line 11649: believe in God perhaps. Your suffering Inquisitor is a mere fantasy.”
Accepted, line 11662: why your Jesuits and Inquisitors have united simply for vile material
Accepted, line 11666: only one like my old Inquisitor, who had himself eaten roots in the desert
Accepted, line 11680: Perhaps nothing but Atheism, that’s all their secret. Your Inquisitor does
Accepted, line 11721: “I meant to end it like this. When the Inquisitor ceased speaking he
Accepted, line 30362: author of a promising poem entitled _The Grand Inquisitor_. I was only
Accepted, line 30365: “I forbid you to speak of _The Grand Inquisitor_,” cried Ivan, crimson
```
---
```
$ ./RegexEngine "(A|a)rriv(al|ed)" samples/the_brothers_karamazov.txt
The following NFA was built:
Initial State: 
4
All States: 
[4, 0, 1, 2, 3, 5, 6, 7, 8, 9, 10, 11, 12, 21, 13, 14, 15, 16, 17, 18, 19, 20]
Accepted States: 
[16, 20]
Transitions: 
(4, 0, epsilon)
(4, 2, epsilon)
(0, 1, 'A')
(2, 3, 'a')
(5, 6, 'r')
(1, 5, epsilon)
(3, 5, epsilon)
(7, 8, 'r')
(6, 7, epsilon)
(9, 10, 'i')
(8, 9, epsilon)
(11, 12, 'v')
(10, 11, epsilon)
(21, 13, epsilon)
(21, 17, epsilon)
(13, 14, 'a')
(15, 16, 'l')
(14, 15, epsilon)
(17, 18, 'e')
(19, 20, 'd')
(18, 19, epsilon)
(12, 21, epsilon)
Accepted, line 780: they gave him, saying that he intended to go third class. On his arrival
Accepted, line 800: returned to our town only three years before Alyosha’s arrival. His former
Accepted, line 815: Pavlovitch might have got into terrible scrapes. Alyosha’s arrival seemed
Accepted, line 1155: The arrival of his two brothers, whom he had not known till then, seemed
Accepted, line 1157: his half‐brother Dmitri (though he arrived later) than with his own
Accepted, line 1253: Our visitors did not take part in the service, but arrived just as it was
Accepted, line 1289: It was strange that their arrival did not seem expected, and that they
Accepted, line 1393: “Here’s the hermitage. We’ve arrived,” cried Fyodor Pavlovitch. “The gates
Accepted, line 1768: awaiting me who arrived before you. But don’t you tell lies all the same,”
Accepted, line 3599: when Miüsov, Kalganov, and Ivan arrived. The other guest, Maximov, stood a
Accepted, line 3986: Alyosha’s arrival. Alyosha “pierced his heart” by “living with him, seeing
Accepted, line 4045: visitors had arrived, including Fyodor Pavlovitch, who was to stand god‐
Accepted, line 4714: whole town, gave suppers and dances. At the time I arrived and joined the
Accepted, line 4755: And then the commander of the division arrived, and kicked up the devil of
Accepted, line 4792: “Suddenly the new major arrived to take command of the battalion. The old
Accepted, line 5016: “Yes, formally and solemnly betrothed. It was all done on my arrival in
Accepted, line 5517: end of dinner, and since Ivan’s arrival in our town he had done so every
Accepted, line 6396: his arrival. Possibly he had been noticed from the window. At least,
Accepted, line 6400: Alyosha thought it strange that his arrival should cause such excitement.
Accepted, line 6518: heard long ago that the money had not arrived. He hadn’t sent the money,
Accepted, line 7239: arrived from town with a singular letter for him from Madame Hohlakov. In
Accepted, line 11878: At last, feeling very cross and ill‐humored, Ivan arrived home, and
Accepted, line 12560: evening, Fyodor Pavlovitch sent for Doctor Herzenstube, who arrived at
Accepted, line 12608: before Alyosha’s arrival; his visitors had gathered together in his cell
Accepted, line 14785: pointed out to all visitors on their arrival with peculiar respect and
Accepted, line 16403: a fatal influence in Grushenka’s life, and whose arrival she was expecting
Accepted, line 16414: in his speedy arrival. Moreover, in the “officer’s” first letter which had
Accepted, line 16581: When he was informed of the arrival of the “captain,” he at once refused
Accepted, line 17088: discussion Mitya got into the trap. Three hours later they arrived. At
Accepted, line 17103: At last they arrived, and Mitya at once ran to Grushenka.
Accepted, line 17892: arrival of this new man, and he had never thought of him! But how could
Accepted, line 18328: waiting for Mitya’s arrival to nail it down and put it in the cart. Pyotr
Accepted, line 18817: peeped out from the steps curious to see who had arrived.
Accepted, line 19169: looked at him very affectionately: before Mitya’s arrival, she had been
Accepted, line 19483: likely be here soon; but the cart with the provisions had not yet arrived.
Accepted, line 19485: but only three girls had arrived, and Marya was not there yet. And he did
Accepted, line 19852: expected cart had arrived with the wines and provisions.
Accepted, line 20945: arrived only five minutes before Pyotr Ilyitch, so that his story came,
Accepted, line 20999: the rural police, Mavriky Mavrikyevitch Schmertsov, who had arrived in the
Accepted, line 21002: “criminal” till the arrival of the proper authorities, to procure also
Accepted, line 21157: first arrival, Mitya had been made very welcome at the police captain’s,
Accepted, line 21414: arrived among us, had from the first felt marked respect for Ippolit
Accepted, line 22192: have done since you arrived?”
Accepted, line 23207: told him, as soon as he arrived, that he had brought three thousand with
Accepted, line 23256: they had not slept all night, and on the arrival of the police officers
Accepted, line 26193: with her. He arrived with her in rain and sleet, sat down on the sofa,
Accepted, line 26197: hour after her arrival. Suddenly she chanced to look at him intently: he
Accepted, line 26454: the first directly he arrived. He galloped here from Moscow at once, of
Accepted, line 26562: Hohlakov heard of his arrival from some one, and immediately sent to beg
Accepted, line 28164: on the first day of his arrival, then he had visited him once more, a
Accepted, line 28174: on Ivan’s going to see them as soon as he arrived in Moscow. But he did
Accepted, line 28175: not go to them till four days after his arrival. When he got the telegram,
Accepted, line 28191: brother. Yet he went to see Mitya on the first day of his arrival, and
Accepted, line 28264: “I only arrived to‐day.... To see the mess you are in here.” Smerdyakov
Accepted, line 30171: “Well, well, what happened when he arrived?”
Accepted, line 30569: drive him away: he disappeared when you arrived. I love your face,
Accepted, line 30722: Visitors had arrived not only from the chief town of our province, but
Accepted, line 30837: At ten o’clock the three judges arrived—the President, one honorary
Accepted, line 31381: advantage of his arrival, and rushed to consult him regardless of expense.
Accepted, line 31546: I have just arrived and have come to thank you for that pound of nuts, for
Accepted, line 34468: with when he arrived here, at his father’s house, and why depict my client
Accepted, line 35774: they all arrived together. Snegiryov opened the door hurriedly and called
```
---
```
$ ./RegexEngine "sir,*" samples/crime_and_punishment.txt
The following NFA was built:
Initial State: 
0
All States: 
[0, 1, 2, 3, 4, 5, 6, 7]
Accepted States: 
[7, 8]
Transitions: 
(0, 1, 's')
(2, 3, 'i')
(1, 2, epsilon)
(4, 5, 'r')
(3, 4, epsilon)
(7, 6, epsilon)
(6, 7, ',')
(8, 6, epsilon)
(5, 8, epsilon)
Accepted, line 159: desire to do so. Nothing that any landlady could do had a real terror
Accepted, line 291: “I remember, my good sir, I remember quite well your coming here,” the
Accepted, line 303: “Step in, my good sir.”
Accepted, line 344: “But that’s for me to do as I please, my good sir, to wait or to sell
Accepted, line 349: “You come with such trifles, my good sir, it’s scarcely worth anything.
Accepted, line 381: “Here, sir: as we say ten copecks the rouble a month, so I must take
Accepted, line 401: “Well, we will talk about it then, sir.”
Accepted, line 407: “What business is she of yours, my good sir?”
Accepted, line 483: felt a desire to be with other people. Something new seemed to be taking
Accepted, line 532: “May I venture, honoured sir, to engage you in polite conversation?
Accepted, line 542: addressed. In spite of the momentary desire he had just been feeling for
Accepted, line 548: I thought! I’m a man of experience, immense experience, sir,” and he
Accepted, line 557: “Honoured sir,” he began almost with solemnity, “poverty is not a vice,
Accepted, line 559: and that that’s even truer. But beggary, honoured sir, beggary is a
Accepted, line 565: Honoured sir, a month ago Mr. Lebeziatnikov gave my wife a beating, and
Accepted, line 594: “Why am I not at my duty, honoured sir,” Marmeladov went on, addressing
Accepted, line 622: “No matter, sir, no matter!” he went on hurriedly and with apparent
Accepted, line 639: if only she felt for me! Honoured sir, honoured sir, you know every man
Accepted, line 653: “Such is my fate! Do you know, sir, do you know, I have sold her very
Accepted, line 702: proud.... And then, honoured sir, and then, I, being at the time a
Accepted, line 708: married me! For she had nowhere to turn! Do you understand, sir, do you
Accepted, line 738: sir, on my own account with a private question. Do you suppose that
Accepted, line 759: her, don’t blame her, honoured sir, don’t blame her! She was not herself
Accepted, line 781: “Since then, sir,” he went on after a brief pause--“Since then, owing
Accepted, line 826: “That was five weeks ago, sir. Yes.... As soon as Katerina Ivanovna
Accepted, line 877: “Honoured sir, honoured sir,” cried Marmeladov recovering himself--“Oh,
Accepted, line 878: sir, perhaps all this seems a laughing matter to you, as it does to
Accepted, line 886: Quite excusable, sir. Well, then, sir” (Marmeladov suddenly gave a sort
Accepted, line 915: you think, my dear sir? For now she’s got to keep up her appearance. It
Accepted, line 919: foot when she has to step over a puddle. Do you understand, sir, do you
Accepted, line 923: me, eh? Are you sorry for me, sir, or not? Tell me, sir, are you sorry
Accepted, line 985: “Let us go, sir,” said Marmeladov all at once, raising his head and
Accepted, line 1004: of.... Know, sir, that such blows are not a pain to me, but even an
Accepted, line 1079: positive con-so-la-tion, ho-nou-red sir,” he called out, shaken to and
Accepted, line 1432: expressing through her his desire to make our acquaintance. He was
Accepted, line 1821: “Do you understand, sir, do you understand what it means when you have
Accepted, line 1847: intently. He felt a sudden desire to find out what it was that was so
Accepted, line 3071: “But why, my good sir, all of a minute.... What is it?” she asked,
Accepted, line 3927: “And pray, what time were you directed to appear, sir?” shouted the
Accepted, line 3944: “Be silent! You are in a government office. Don’t be impudent, sir!”
Accepted, line 4112: Raskolnikov had a sudden desire to say something exceptionally pleasant
Accepted, line 4139: “Nobody asks you for these personal details, sir, we’ve no time to
Accepted, line 4827: sir. That was Alexey Semyonovitch; he is in our office, too.”
Accepted, line 4831: “Yes, indeed, sir, he is of more weight than I am.”
Accepted, line 4841: know him, sir?”
Accepted, line 6009: Pyotr Petrovitch, “and desire for good exists, though it’s in a childish
Accepted, line 6071: “Excuse me, sir,” said Luzhin, affronted, and speaking with excessive
Accepted, line 6074: “Oh, my dear sir... how could I?... Come, that’s enough,” Razumihin
Accepted, line 6217: you, sir,” he began deliberately, doing his utmost to restrain himself
Accepted, line 6418: trilled the thin voice of the singer. Raskolnikov felt a great desire to
Accepted, line 6447: “I say, sir,” the girl shouted after him.
Accepted, line 6497: “Yes, sir, here’s to-day’s. No vodka?”
Accepted, line 6629: desire to shout at them, to swear at them, to put out his tongue at
Accepted, line 6688: Raskolnikov had an intense desire again “to put his tongue out.” Shivers
Accepted, line 6845: you see that I don’t want your benevolence? A strange desire you have to
Accepted, line 8397: slightest desire to enter into more personal relations with the two
Accepted, line 8886: visit to him in his illness yesterday, and, moreover, since I desire
Accepted, line 9578: life)--but to the widow. In all this I see a too hasty desire to slander
Accepted, line 10255: and such things belong to you, and that you desire to redeem them...
Accepted, line 11289: obey, trembling creation, and not _to have desires_, for that’s not for
Accepted, line 12115: desire to do so, I was unable to meet you yesterday. But I trust all
Accepted, line 12152: uneasiness, unless, of course, you are yourselves desirous of getting
Accepted, line 12222: died so strangely, is a terrible instance. My only desire has been to be
Accepted, line 12283: certainly desired an explanation with you and your honoured mother upon
Accepted, line 12286: desire and am not able to speak openly... in the presence of others...
Accepted, line 12401: “Excuse me, sir,” said Luzhin, quivering with fury. “I enlarged upon
Accepted, line 12434: Petrovitch. Dounia has told you the reason your desire was disregarded,
Accepted, line 12436: laying commands upon me. Are we to consider every desire of yours as
Accepted, line 12450: “But now in any case I cannot reckon on it, and I particularly desire
Accepted, line 12633: “He wants to make you a present of ten thousand roubles and he desires
Accepted, line 13429: dread and suffering, yet she had a tormenting desire to read and to read
Accepted, line 13805: irritation, “yesterday you expressed a desire that I should come to you
Accepted, line 14023: dear sir, are weighty matters and it’s astonishing how they sometimes
Accepted, line 14241: expression) saying: ‘And what were you doing, sir, pray, at ten or
Accepted, line 14266: all right, but why, my good sir, in your illness and in your delirium
Accepted, line 15281: is always arranged in such cases by friends or even outsiders desirous
Accepted, line 15381: desire you to respect me. See!’ Am I not right?”
Accepted, line 15444: continual failures and misfortunes she had come to desire so _keenly_
Accepted, line 16249: you are lying, sir. You are lying and slandering from some spite against
Accepted, line 17524: “I thank you, honoured sir,” she began loftily. “The causes that have
Accepted, line 17527: You see, honoured sir, these orphans of good family--I might even say of
Accepted, line 17551: “Honoured sir, honoured sir, you don’t know,” screamed Katerina
Accepted, line 18264: reason to like me. You may think what you like, but I desire now to do
Accepted, line 19242: my side with a most irresistible physical desire. Avdotya Romanovna is
Accepted, line 19529: Only _adieu, mon plaisir_, may we meet again.”
Accepted, line 20347: “Yes, sir.”
Accepted, line 20440: desired to avenge myself even, and that’s a bad sign, a bad sign, a bad
Accepted, line 21558: his miserable position, his poverty and helplessness, and his desire to
Accepted, line 21568: but had rather shown a desire to exaggerate his guilt. All the strange
Accepted, line 21825: more. Perhaps it was just because of the strength of his desires that he
Accepted, line 21861: desire to live so strong and was it so hard to overcome it? Had not
```
---
```
$ ./RegexEngine "Alyosha and (Ivan|Dmitri)" samples/the_brothers_karamazov.txt
The following NFA was built:
Initial State: 
0
All States: 
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 44, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43]
Accepted States: 
[31, 43]
Transitions: 
(0, 1, 'A')
(2, 3, 'l')
(1, 2, epsilon)
(4, 5, 'y')
(3, 4, epsilon)
(6, 7, 'o')
(5, 6, epsilon)
(8, 9, 's')
(7, 8, epsilon)
(10, 11, 'h')
(9, 10, epsilon)
(12, 13, 'a')
(11, 12, epsilon)
(14, 15, ' ')
(13, 14, epsilon)
(16, 17, 'a')
(15, 16, epsilon)
(18, 19, 'n')
(17, 18, epsilon)
(20, 21, 'd')
(19, 20, epsilon)
(22, 23, ' ')
(21, 22, epsilon)
(44, 24, epsilon)
(44, 32, epsilon)
(24, 25, 'I')
(26, 27, 'v')
(25, 26, epsilon)
(28, 29, 'a')
(27, 28, epsilon)
(30, 31, 'n')
(29, 30, epsilon)
(32, 33, 'D')
(34, 35, 'm')
(33, 34, epsilon)
(36, 37, 'i')
(35, 36, epsilon)
(38, 39, 't')
(37, 38, epsilon)
(40, 41, 'r')
(39, 40, epsilon)
(42, 43, 'i')
(41, 42, epsilon)
(23, 44, epsilon)
Accepted, line 28134: slowly homewards. Both Alyosha and Ivan were living in lodgings; neither
Accepted, line 31041: excepting Alyosha and Ivan, but he obtained no exact information from any
```
---
```
$ ./RegexEngine "Russia(n)*" samples/the_idiot.txt
The following NFA was built:
Initial State: 
0
All States: 
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
Accepted States: 
[13, 14]
Transitions: 
(0, 1, 'R')
(2, 3, 'u')
(1, 2, epsilon)
(4, 5, 's')
(3, 4, epsilon)
(6, 7, 's')
(5, 6, epsilon)
(8, 9, 'i')
(7, 8, epsilon)
(10, 11, 'a')
(9, 10, epsilon)
(13, 12, epsilon)
(12, 13, 'n')
(14, 12, epsilon)
(11, 14, epsilon)
Accepted, line 89: neighbour had been obliged to bear the full severity of a Russian
Accepted, line 93: the long cold journey through Russia, from Eydkuhnen to St. Petersburg.
Accepted, line 105: un-Russian.
Accepted, line 129: been long absent from Russia, more than four years; that he had been
Accepted, line 145: is to get hold of our good Russian money free, gratis, and for nothing.”
Accepted, line 249: “No, I don’t--not at all! I hardly know anyone in Russia. Why, is that
Accepted, line 764: the houses--a Russian can’t live in them in the winter until he gets
Accepted, line 777: “You must have forgotten Russia, hadn’t you?”
Accepted, line 780: wonder at myself for not having forgotten how to speak Russian? Even
Accepted, line 784: on and on talking Russian.”
Accepted, line 1002: coming. You see I have not been in Russia for four years, and knew very
Accepted, line 1139: despatched the young man to Russia.
Accepted, line 1143: “Then you have no one, absolutely _no_ one in Russia?” he asked.
Accepted, line 1156: Russian books.”
Accepted, line 1158: “Russian books, indeed? Then, of course, you can read and write quite
Accepted, line 1277: “Yes, I do! I have only been one day in Russia, but I have heard of
Accepted, line 1389: have tried to translate the French character into the Russian letters--a
Accepted, line 1392: all.’ That is the script of the Russian War Office. That is how official
Accepted, line 1680: to an estate of Totski’s, in one of the central provinces of Russia,
Accepted, line 1699: forgot all about the child; but five years after, returning to Russia,
Accepted, line 2280: they took me away from Russia, I remember I passed through many German
Accepted, line 3110: indeed, I was far from thinking that I should ever return to Russia.
Accepted, line 5812: nowadays? Especially here, in our dear Russia. How it has happened I
Accepted, line 6456: in real Russian style. Well, when I began cursing at her, a strange
Accepted, line 6574: pay it in there for you with pleasure.’ I liked that old fellow, Russian
Accepted, line 6740: out, did not understand a word of Russian, and seemed to be as stupid as
Accepted, line 6810: he exhibited, as if by accident, that peculiarly Russian object--an
Accepted, line 7819: flying somewhere into the interior of Russia this time, and that
Accepted, line 9182: lying before me. ‘What! have you begun to read Russian history?’ she
Accepted, line 9184: Solovieff’s Russian History and read it, because I knew nothing. ‘That’s
Accepted, line 9374: unbelievers nowadays, especially Russians, I have been told. You ought
Accepted, line 9436: a tremendous impression upon me. I had understood nothing about Russia
Accepted, line 9463: seen in the heart of a Russian. This is a conviction which I have gained
Accepted, line 9464: while I have been in this Russia of ours. Yes, Parfen! there is work to
Accepted, line 9465: be done; there is work to be done in this Russian world! Remember what
Accepted, line 9735: about the murder, and that quite recently. Since he came to Russia, he
Accepted, line 9743: a passionate faith in the Russian soul, however, and what discoveries he
Accepted, line 9745: soul is a mystery, and depths of mystery lie in the soul of a Russian.
Accepted, line 10167: hundred on the thousandth anniversary of the foundation of the Russian
Accepted, line 10177: the two hundred guests and the thousandth anniversary of the Russian
Accepted, line 10584: “It’s simply that there is a Russian poem,” began Prince S., evidently
Accepted, line 10978: is not a question of showing that Pushkin is stupid, or that Russia must
Accepted, line 11037: the purest Russian blood ran in his veins. Lebedeff’s nephew, whom
Accepted, line 11149: “Strange things are going on in our so-called Holy Russia in this age of
Accepted, line 11164: Russia, wearing gaiters like a foreigner, and shivering with cold in
Accepted, line 11169: his story proves the truth of the Russian proverb that ‘happiness is
Accepted, line 11175: of a very rich Russian landowner. In the good old days, this man,
Accepted, line 11180: to have been one of those Russian parasites who lead an idle existence
Accepted, line 11184: least a third of the money paid by Russian peasants to their lords in
Accepted, line 11190: pupil could not speak in any language, not even Russian. But ignorance
Accepted, line 11210: shabby cloak and packed him off to Russia, third class. It would seem
Accepted, line 11262: children of Russian merchants at ten copecks a lesson, especially with
Accepted, line 11587: speak and understand Russian, though),--but now I can appreciate what I
Accepted, line 11796: well aware, has never been out of Russia.... It is too late to read the
Accepted, line 11834: the greater part of his life out of Russia, returning at intervals for
Accepted, line 13848: aristocratic family. True, Russians think more of influential friends
Accepted, line 14060: conservatism; but I am attacking _Russian_ liberalism; and I attack it for
Accepted, line 14061: the simple reason that a Russian liberal is not a Russian liberal, he is
Accepted, line 14062: a non-Russian liberal. Show me a real Russian liberal, and I’ll kiss him
Accepted, line 14082: “How, nothing that they have done is Russian?” asked Prince S.
Accepted, line 14084: “It may be Russian, but it is not national. Our liberals are not
Accepted, line 14085: Russian, nor are our conservatives, and you may be sure that the nation
Accepted, line 14098: certainly do hold that Russian literature is not Russian, except perhaps
Accepted, line 14108: really national. If any Russian shall have done or said anything really
Accepted, line 14110: though he may not be able to talk the Russian language; still he is a
Accepted, line 14111: national Russian. I consider that an axiom. But we were not speaking
Accepted, line 14113: I insist that there does not exist one single Russian socialist. There
Accepted, line 14145: fact is expressed the whole essence of Russian liberalism of the sort
Accepted, line 14151: consists in this, that _Russian_ liberalism is not an attack upon the
Accepted, line 14154: Russian order of things, but on Russia itself. My Russian liberal
Accepted, line 14155: goes so far as to reject Russia; that is, he hates and strikes his own
Accepted, line 14157: mirth, and even with ecstasy. He hates the national customs, Russian
Accepted, line 14159: not know what he is doing, and believes that his hatred of Russia is the
Accepted, line 14163: aware of the fact.) This hatred for Russia has been mistaken by some of
Accepted, line 14164: our ‘Russian liberals’ for sincere love of their country, and they
Accepted, line 14175: my original statement that a Russian liberal is _not_ a _Russian_
Accepted, line 14190: more or less right, and that Russian liberalism--that phase of it which
Accepted, line 14192: Russia itself, and not only its existing order of things in general. Of
Accepted, line 14291: than the exception, unfortunately for Russia. So much so, that if this
Accepted, line 14297: times, and not only here in Russia, but everywhere else as well. And in
Accepted, line 17363: the criminals, all over Russia and Siberia, knew him!
Accepted, line 17473: Russian); so that maybe he was not so far from my final conviction as
Accepted, line 19243: uniform [Civil Service clerks in Russia wear uniform.]--you must have
Accepted, line 20980: being full of self-respect, in which quality the ordinary Russian is so
Accepted, line 21508: strange disclosures is to be gained the full knowledge of Russian life
Accepted, line 21535: “To this keen question I replied as keenly, ‘The Russian heart can
Accepted, line 21539: his suite: ‘I like that boy’s pride; if all Russians think like this
Accepted, line 21621: the Russians, and he would have forgotten all about me had he not loved
Accepted, line 21643: “‘Child,’ he said, abruptly. ‘If I were to recognize the Russian
Accepted, line 21644: orthodox religion and emancipate the serfs, do you think Russia would
Accepted, line 21652: fiat of the Russian people. Enough, Davoust, it is mere phantasy on our
Accepted, line 21990:  no one knew what the position of a respectable person in Russia would
Accepted, line 22879: Russia, or about Beauty redeeming the world, or anything of that sort,
Accepted, line 23292: of those Olympian administrators who know everything except Russia,
Accepted, line 23335: a poet, German by name, but a Russian poet; very presentable, and even
Accepted, line 23340: Russian verse, and claimed to have been a friend of a famous Russian
Accepted, line 23696: Russian civilization to _them_, we must stand before them, not letting it
Accepted, line 23730: them. We Russians no sooner arrive at the brink of the water, and
Accepted, line 23737: “Our Russian intensity not only astonishes ourselves; all Europe wonders
Accepted, line 23746: of vanity that Russians become Atheists and Jesuits! But from spiritual
Accepted, line 23749: never knew it. It is easier for a Russian to become an Atheist, than for
Accepted, line 23750: any other nationality in the world. And not only does a Russian ‘become
Accepted, line 23760: “But let these thirsty Russian souls find, like Columbus’ discoverers, a
Accepted, line 23761: new world; let them find the Russian world, let them search and discover
Accepted, line 23763: Show them the restitution of lost humanity, in the future, by Russian
Accepted, line 23764: thought alone, and by means of the God and of the Christ of our Russian
Accepted, line 23980: stratum of Russian society is _worthless_, has outlived its time, has
Accepted, line 24001: me persons who can understand, who can forgive--kind, good Russian
Accepted, line 24007: among us--it may be the order elsewhere, but not in Russia. Surely you
Accepted, line 25077: hardly talk Russian, but had fallen in love with one of the Miss
Accepted, line 25333: in Switzerland, for your home-country, for Russia; you read, doubtless,
Accepted, line 25334: many books about Russia, excellent books, I dare say, but hurtful to
Accepted, line 25579: to Lebedeff that this was the first time he had ever heard a Russian
Accepted, line 25756: his life--abroad, if necessary. There are Russian priests everywhere,
Accepted, line 26839: in Russia, visits his sick friend at Schneider’s every few months.
Accepted, line 26916: I’ve had a good Russian cry over this poor fellow,” she added, pointing
```
