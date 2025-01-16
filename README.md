A tentative title for the project:
Decrypting Cryptic Crosswords: Semantically Complex Wordplay Puzzles as a Target for NLP

Brief description of project goals and proposed methods:
Our team has tentatively finalized to replicate the results of the paper “Decrypting Cryptic Crosswords: Semantically Complex Wordplay Puzzles as a Target for NLP”, see [1] for our final project, and attempt to solve the whole crossword puzzles if time permits. We will have to introduce grid constraints in our algorithms to do this. We would also like to implement self-consistency in the chain of thought reasoning to charades and double definition clue structures as presented in [3].

The authors of the paper “Decrypting Cryptic Crosswords: Semantically Complex Wordplay Puzzles as a Target for NLP'', see [1] J.Rozner et al.(November 2021), attempted to use three baselines to create an NLP model- T5, Transformer-based encoder-decoder, and neural baseline to solve cryptic crossword clues which have been classified into five categories. The authors have categorized the crossword clues to be of these five types, namely- Anagram, Initialise, Hidden, Charade, and Double Definition. An Anagram clue requires the scrambling of a word to create another word. The clue sentence must be categorized as an Anagram clue to perform the jumbling of the Anagram clue word. Initialism requires considering the first letter of every word in the clue sentence to make a clue word. Hidden clue sentences would have the clue word in the phrases of the sentence. The Charade clue sentences have a sequence of clues for the final answer. Finally, in the Double Definition, two synonyms or phrases appear adjacent to each other in the clue sentence and they can refer to the final answer. The Charade and Double Definition do not have any indicators to classify the clues into them. Individual clue types were taken to solve them instead of solving the whole crossword puzzle, as cryptic clues find less reliability on the grid constraint because of the uniqueness of the answers. The dataset that was used by the authors was from thegaurdian.com consisting of 142380 clues. The authors of [1] used a learning approach before solving the cryptic clues which included fine-tuning the model on related, and synthetic tasks like descrambling an augmented word task before solving the cryptic clues. This was done to improve a T5 seq-to-seq approach.

Proposed method:
Firstly the problem is framed as a seq-to-seq task from the input clues. J.Rozner et al. (November 2021) explain this with an example- “But everything’s really trivial, initially, for a transformer model”- here the indicator word is - “initially”, which must trigger the algorithm to take the initial letters of the sentence to prepare the output word for the puzzle or as the next clue input, which is BERT. After creating a framework for the task- the next in process three splits were considered by the authors- naive, disjoint, and word-initial disjoint split. The naive is a 60 per cent random split for train, 20 for dev, and 20 for the test; the disjoint split has all clues with the same answer appear in one train, dev, and test set; for word-initial disjoint split, the authors used clues to train, dev and test with answers that have same first two letters. (Here we would like to entertain an experiment where we use clues that have a 50% match to letters of answers to compare).
The metrics used in the experiment by J.Rozner et al. (November 2021) were:
To check the length of the top answers and if they match the length of the correct answer by checking the enumeration. Enumeration is the number or numbers in the parentheses indicating the count of letters in the answer word. It is at the end of the clue. Example- (3) or (4,8)
To check how often the correct answer appears in the top ten answers. 

The non-neural baselines that were used by J. Rozner et al.(November 2021):
WordNet: This baseline worked well for cryptic clues where its definition either appeared at the beginning or the end. Here, the reverse dictionary outputs are taken for beginning and end words in the clue and the outputs for this search are ranked through character overlaps with the rest of the clue.
KNN BoW: This baseline was used by the authors to determine if the clues that are in the same lexical space have similar answers. KNN was used on top of the BoW featurizer.
Rule-based: This uses WordNet’s word similarity function to rank outputs. Deits solver was used [2] by J. Rozner et al.(November 2021). Deits solver handles initialism, anagrams, substrings, insertions, and reversals using Rules. This does not work with clue types- charade, and double definition.
T5 vanilla seq2seq: Here J. Rozner et al.(November 2021) fine-tuned the Transformer-based T5-base model with HuggingFace’s pre-trained model parameters. The finetuning was done by supervised learning. At the test, the outputs were generated using beam search. The metric was used to further establish the correctness of the output answer.

Curricular learning technique: Here the authors J. Rozner et al.(November 2021), use synthetic datasets to train models to learn wordplay indicators, perform wordplay operations, etc. Labels were used on the synthetic dataset to perform the curricular learning operations. The labels used are for tasks:
ACW (American CrossWord): Input-output clues
ACW-descramble: here the cryptic clue is scrambled and appended to the clue sentence
ACW-descramble-word, unscramble the answer words
Anagrams: used indicators to call a clue an anagram


The results of the experiment conducted by J. Rozner et al.(November 2021) revealed when the naive split was used that the results were far better than 2 word-initial disjoint splits.


Model
Top Correctness % (test)
Top 10 correctness % (test)
WordNet
2.6
10.7
Rule-based
7.3
14.7
KNN (no length)
5.6
10.1
KNN (length)
6.1
11.3
T5(no length)
15.6
30.0
T5 (length)
16.3
33.9
Curricular: ACW + ACW-descramble
21.8
42.4

Table 1.1: Results table with naive-split of the ACW dataset. 

Our contribution (if time permits, after replicating the results of the paper):
The curricular learning finetunes the T5 model to make sure that sub-parts of the problem are learnt. Our team would like to re-experiment this setting and make changes after further research. We would like to understand if a hybrid model of Rule-based and T5 would increase the process while maintaining accuracy. We plan to make changes to the Deits [2] code that is available to implement curricular learning and further catch charade and double-definition clues- by using Rule within a Rule system.
In the word-initial disjoint split technique, the authors used clues to train, dev and test with answers that have the same first two letters. We would like to entertain an experiment where we use clues that have a 50% match to letters of answers to compare.
We in particular want to implement self-consistency in the chain of thought reasoning to the charade and double definition clue structures using methods established in [3] by X. Wang et al. (October 2022). We would like to use symbolic and common sense reasoning for the mentioned classifications of clues.


References: 
[1]  J. Rozner, C. Potts, and K. Mahowald, “Decrypting Cryptic Crosswords: Semantically Complex Wordplay Puzzles as a Target for NLP.” arXiv, 2021. doi: 10.48550/ARXIV.2104.08620.
[2]  Robin Deits. rdeits/cryptics, 2015. URL https://github.com/rdeits/cryptics.
[3]  X. Wang et al., “Self-Consistency Improves Chain of Thought Reasoning in Language Models.” arXiv, 2022. doi: 10.48550/ARXIV.2203.11171.

