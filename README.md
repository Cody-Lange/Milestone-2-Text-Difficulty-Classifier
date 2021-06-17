# Milestone-2---Text-Difficulty-Classifier

**Supervised Learning Methods**

In many real-world applications, there is a need to make sure textual information is comprehensible/readable by audiences who may not have high reading proficiency. This might include students, children, adults with learning/reading difficulties, and those who have English as a second language. The Simple English Wikipedia (https://en.wikipedia.org/wiki/Simple_English_Wikipedia), for example, was created exactly for this purpose. Before the editors spend a lot of effort to simplify the text and increase its readability, it would be very useful to suggest to them which parts of an article's text might need to be simplified.

This notebook develops and trains a Multinomial Naive Bayes classifier, a logistic regression model, and gradient boosted decision trees classifier to address the challenge of binary text classification.

Sentences from Wikipedia articles are classified into one of two categories:

0: the sentence does NOT need to be simplified.

1: the sentence DOES need to be simplified.

The training data contains 416,768 sentences, already labeled with one of the above categories. The test data contains 119,092 comments that are unlabeled. (The test data is strictly used for the class pseudo competition.)

**Cleaning**

The following CSVs and text files were imported via the Pandas library:

**WikiLarge_Train.csv -** This CSV was obtained from The simple Wikipedia (https://en.wikipedia.org/wiki/Simple_English_Wikipedia) and contains 416,768 lines of text with labels of 0 to 1 denoting whether the line of text was complex or not. No cleaning was needed other than to load the CSV as a Pandas dataframe.

**Dale_chall.txt -** This text file obtained from 

https://www.readabilityformulas.com/articles/dale-chall-readability-word-list.php  contains approximately three thousand familiar words that are known in reading by at least 80 percent of the children in Grade 5. Pandas was able to easily load the text file as a dataframe, and the values were then flattened and converted into  a list.

**AoA_51715_words.csv -** This CSV obtained from http://crr.ugent.be/archives/806  contains "Age of Acquisition" (AoA) estimates for about 51k English words, which refers to the approximate age (in years) when a word was learned. The csv was loaded as a dataframe, and information pertaining to words, age of acquisition, and syllables were put in a dictionary. 

**Concreteness_ratings_Brysbaert_et_al_BRM.txt -** This text file obtained from http://crr.ugent.be/papers/Brysbaert_Warriner_Kuperman_BRM_Concreteness_ratings.pdf contains concreteness scores for 40 thousand generally known English word lemmas. The text was loaded via Pandas, and information pertaining to a lemma’s concreteness score and recognizability was stored in a dictionary. 

**Pre-Processing**

**Feature Selection**

After the relevant data was loaded, two different feature sets were created to give more information for the models to make classifications on. Both sets included, age of acquisition, concreteness, word count, average word length, syllable counts and averages, recognizability, and parts of speech. However, one set represents the text as a Tf-idf bag of words, and the other set represents the text as Word2Vec embeddings. Here is more information about the features generated

**Age of Acquisition (AoA) -** Age of acquisition refers to the approximate age in years when a word was learned. Early words, being more basic, have lower AoA scores, so the average age of acquisition of the text was included, along with the percent of words being under age 5, 10, 15, 20, and greater than 20. The rationale is that easier documents to read will have lower age of acquisition scores.

**Concreteness -** Concreteness evaluates the degree to which the concept denoted by a word refers to a perceptible entity. Concrete words are easier to remember than abstract words, because they activate perceptual memory codes in addition to verbal codes. A concrete word comes with a higher rating and refers to something that exists in reality; you can have immediate experience of it through your senses (smelling, tasting, touching, hearing, seeing) and the actions you do. Hence, having more words with a higher concreteness value would make a sentence simpler.

**Word Count -** The number of words in the line of text. Simpler texts likely have less words.

**Average word Length -** As stated. Simpler texts likely have smaller words on average.

**Average Syllable Count and Groupings -** Syllables are the phonological building blocks of words and are single units of speech, either as a whole word or one of the parts into which a word can be separated, and they  usually contain a vowel. Naturally, words with more syllables are more complex. For this data, the percentages of words that have one through four syllables and more than 5 syllables are represented, as well as the average syllable count for the sentence.
The NLTK library provides the most accurate means of getting syllable count; however, using NLTK is inefficient, so I first checked the AOA dictionary first to see if syllable counts are there. Lastly, if a syllable is not even accounted for,  a function was written to algorithmically determine syllable count based off of vowels, although this method can be inaccurate for exceptional words.

**Recognizability -** Percentage participants who knew the word in the _Brysbaert_et_al_ study from the concreteness csv. 

**% Parts of Speech -**  Parts of Speech are the categories to which a word is assigned in accordance with its syntactic functions. They are essential for breaking down the structure of text, so there is possibly a relationship between the diversity and counts of parts of speech tag and text complexity. 

**Term Frequency-Inverse Document Frequency (Tf-idf) -** A Tf-idf vectorizer numerically represents the texts as a “bag of words” by measuring term frequency and inverse document frequency. Term frequency gives weight to words that appear more often, and inverse document frequency gives more weight to words that appear in fewer documents. I hypothesize that this is advantageous due to big words that are harder to read being in fewer documents, and more simple words appearing in relatively more documents. The frequency of the word may somehow be related to the complexity. 
The Tf-idf vectorizer class from scikit-learn also allows us to remove common stopwords and put the words in lowercase. Since the model is checking for readability, it is okay to put the words in lowercase, since the capitalization doesn't affect readability, and keeping track of less words frees up memory.

**Word2Vec Embeddings -** Word2Vec provides vectorized representations of each word in the text, and words that are similar in meaning have similar representations. Additionally, the vectorized representations manage to capture their meanings, semantic relationships and the different types of contexts they are used in. The context of words and how they're used may have a relationship with a difficulty to understand them, so Word2Vec may be a fitting representation of the text.
