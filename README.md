# natural_bruteforce_wordlists

Randomly generated character sequences for mask attacks generate many words that are unlikely to be natural words based on the sequence of letters. This is an attempt to shorten these word lists by matching these types of sequences and removing them with tools lie grep.

Mask Attacks try all combinations from a given keyspace just like in Brute-Force attack, but more specific:
https://github.com/hashcat/maskprocessor

Output of a mask generated wordlist may look like:
Aabml76
Aabml77
Aabml78
Aabml79
Aabml80
Aabml81
Aabml82

Sequences like 2 'a's in a row or 3 consonants in a row like 'bml' as seen in these examples are unlikely to appear in natural words, or made up ones. 

The grep commands below can be used alone or in series to remove strings which are unlikely to be words based on character patterns:

Remove lines with characters appearing 3 or more times in a row: 
grep -Ev "(.)(.*\1){2,}"

Remove lines with duplicate characters that are rare to see as duplicate characters: : 
grep -Ev '([abfhijkquvwxyABFHIJKQUVWXY])\1{1}'

Remove lines with 3 consecutive consonants which rarely appear in 3s. 'S' has been removed as it often appears in doubles before or after another consonant ('PASSWORD'), or alone near pairs of consonants ('Jumpshot'), as well as the letter 'k' as a middle letter (for words like Jackpot, Corckscrew): 
grep -vE '[bcdfghjklmnpqrtvwxzBCDFGHJKLMNPQRTVWXZ][bcdfghjlmnpqrtvwxzBCDFGHJLMNPQRTVWXZ][bcdfghjklmnpqrtvwxzBCDFGHJKLMNPQRTVWXZ]'
