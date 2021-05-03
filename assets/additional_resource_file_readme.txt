
== dale_chall.txt ==

This is the Dale Chall 3000 Word List, which is one definition of words that are considered "basic" English.
A summary is at https://www.readabilityformulas.com/articles/dale-chall-readability-word-list.php


== Concreteness_ratings_Brysbaert_et_al_BRM.txt ==

This file contains concreteness ratings for 40 thousand English lemma words gathered via Amazon Mechanical Turk. The ratings come from a larger list of 63 thousand words and represent all English words known to 85% of the raters.

The file contains eight columns:
1. The word
2. Whether it is a single word or a two-word expression 
3. The mean concreteness rating
4. The standard deviation of the concreteness ratings
5. The number of persons indicating they did not know the word
6. The total number of persons who rated the word
7. Percentage participants who knew the word
8. The SUBTLEX-US frequency count (on a total of 51 million; Brysbaert & New, 2009) 
9. The dominant part-of-speech usage

Original source: http://crr.ugent.be/archives/1330

Brysbaert, M., Warriner, A.B., & Kuperman, V. (2014). Concreteness ratings for 40 thousand generally known English word lemmas. Behavior Research Methods, 46, 904-911.
http://crr.ugent.be/papers/Brysbaert_Warriner_Kuperman_BRM_Concreteness_ratings.pdf


== AoA_51715_words.csv ==

This file contains "Age of Acquisition" (AoA) estimates for about 51k English words, which refers to the approximate age (in years) when a word was learned. Early words, being more basic, have lower average AoA.

The main columns you will be interested in are "Word" and "AoA_Kup_lem". But the others may be useful too.

The file contains these columns:

Word :: The word in question
Alternative.spelling :: if the Word may be spelled frequently in another form	
Freq_pm	:: Freq of the Word in general English (larger -> more common)
Dom_PoS_SUBTLEX	:: Dominant part of speech in general usage
Nletters :: number of letters 
Nphon :: number of phonemes
Nsyll :: number of syllables
Lemma_highest_PoS :: the "lemmatized" or "root" form of the word (in the dominant part of speech. e.g. The root form of the verb "abates" is "abate".
AoA_Kup	:: The AoA from a previous study by Kuperman et al.
Perc_known :: Percent of people who knew the word in the Kuperman et al. study
AoA_Kup_lem :: Estimated AoA based on Kuperman et al. study lemmatized words. THIS IS THE MAIN COLUMN OF INTEREST.
Perc_known_lem	:: Estimated percentage of people who would know this form of the word in the Kuperman study.
AoA_Bird_lem :: AoA reported in previous study by Bird (2001) 
AoA_Bristol_lem	:: AoA reported in previous study from Bristol Univ. (2006)
AoA_Cort_lem :: AoA reported in previous study by Cortese & Khanna (2008)
AoA_Schock :: AoA reported in previous study by Schock (2012)

Original source : http://crr.ugent.be/archives/806
