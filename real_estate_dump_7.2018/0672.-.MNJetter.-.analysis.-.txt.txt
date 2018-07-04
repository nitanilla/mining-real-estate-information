How to use these scripts:

---------------

NOTE: Unless otherwise specified, all scripts require Python 2.7 and NLTK v3 (py27-nltk on Macports), and must be run in the same directory as the target transcript document.

---------------

NCC.PY

Function: Gets a concordance, or a list, of a target word as it shows up in the transcript with the target word in the middle surrounded by 25 characters of context on either side of each instance.

How to use: Run in the command line as follows.
$ python2.7 ncc.py fname textword

(fname = file name, such as transcript.txt)
(textword = the target word to get a concordance for)

Example output (target word "innovating"):
> Displaying 4 of 4 matches:
> ng our products and , we 'll keep innovating and keep putting new stuff inside
>  a trajectory of improvement that innovating , that customers are able to util
> nt trajectory of improvement that innovating companies provide as they keep in
> ause that was their mindset , was innovating and being entrepreneurs . And eve

---------------

NCL.PY

Function: Gets a list of possible collocations, or words that show up together frequently in the text and may be related as a phrase.

How to use: Run in the command line as follows.
$ python2.7 ncl.py fname

(fname = file name, such as transcript.txt)

Example output:
> little bit; New York; Silicon Valley; United States; San Francisco; real estate; make sure; Hong Kong; 've got; business model; years ago; would say; educational background; social media; company culture; Edison Awards; anything else; target audience; good luck; every day