### Introduction

Out of vocalbulary words are a serious issues in the language models. Out of vocalbulary words are terms that are not a part of the normal lexicons in a NLP environment. When a word is not available in the training data , but appears in the testing set. The main issue with it is the models assigns a prbaibility of zero leadins to a zero likelihood as well as lowering the model performance. Spme attempts have been made in the past to estimate representations of OOV words. One used external auxilary information where the disadvantage was that you will need an external information. Another way was to embed words that takes OOV words and maps them into a vectore representation. In this project we are analyzing the oov word embedding based on subwords on 2 language data. One is Englishe text another is Bengali language text.

### Required Steps

For this project work we will be requiring following steps:

1.   Selecting appropiate subwords from the given corpus
2.   Building a Language Model by training RNN over the subwords.

3. Generate larger corpus using the language models

4. Compareing OOV rates and performing hyperparameter tuning

### Data Preprocessing

As we are using a tool named sentencePiece to select subwords from a corpus we need to pass raw sentence as an input. Therefore we need to process our dataset. For both language data we select each sentence and store it in a file separating with a signle line. After preprocessing we are splitting the total data in to 80-20 ratio of training and testing data.  We store it as train.txt and test.txt for each language.

### Subword Segmentation

We are using the SentencePiece implementation of BPE. At first we are training the sentencePiece model with a specified vocabulary size. For our task we consider 3 types of subword granularity, character level, small vocab, large vocab. After checking different sizes we selected following vocab size for English and Bengali language;
1. English Char level = input alphabet size, small vocab = 500, large vocab =2400

2. Bengali Char level = input alphabet size, small vocab = 700, large vocab =1500

For Bengali corpus the large vocab size seems to be confined to 1800. As putting more than that will throw an error. 

Next we encoded our texts using the model we trained earlier to generate our subwords. For each language we created 3 models so we got 6 subword segmentation files in the end. 

After comparing all the subwords we can understand that English corpus produced dataset with a assigned  subword granularity correctly. For character level each of the characters were separated including all the stop words as we passed the whole raw sentence as input we preffered to keep those words. For Bengali data it was a little different. As Bengali character not only consist of alphabet instead they have a lot of extra subcharacters that are not characters but are needed to make a word meaaningful there fore the character size were larger than the English and the output didn't follow the subword granularity in some cases. 

### Language Model using RNN

In this step we are training 3 language models for each language from the earlier corpora. We are using RNNLM toolkit. The perforemance depends on number of hidden latets, back propagation parameters. For implementing class based language model we use class size. After training the RNNNLM outputs perplexity of the training model. We tune the parameters to achieve perplexitiy below than baseline. We can see the perplexity for each language below,

#### English Corpora

  * baseline s1 Train Entropy 3.2338 Valid Entropy 5.408 alpha =.025
  * baselone s2 train Entropy 7.6375 Valid Entropy 8.1982 alpha =.05
  * baseline s3 train Entropy 7.6280 valid Entropy 9.3615 alpha =.05
  

Our results ( increased hidden layers to 128, selecting classsize as 200,500,900)

* tuned s1 Train Entropy 3.2128 Valid Entropy 5.3745 alpha =.05
* tuned s2 train Entropy 7.6315 Valid Entropy 7.9883 alpha =.025
* tuned s3 train Entropy 7.5352 valid Entropy 9.2545 alpha =.025

#### Bengali Corpora

  * baseline s1 Train Entropy 4.3710 Valid Entropy 8.0988 alpha =.025
  * baselone s2 train Entropy 5.7609 Valid Entropy 9.8194 alpha =.05
  * baseline s3 train Entropy 7.6280 valid Entropy 9.3615 al[ha = 0.003


Our results ( increased hidden layers to 128, selecting classsize as 200,500,900)

* tuned s1 Train Entropy 3.9922 Valid Entropy 8.0063  alpha =.00625
* tuned s2 train Entropy 5.7361 Valid Entropy 9.6414  alpha =.025
* tuned s3 train Entropy 6.5691 valid Entropy 10.6734 alpha =.025


### Text Generation


For text generation we are using rnnlm toolkit. They include generating function where we are inputting the LM models and the size and it will generate accordingly. After generation it still stays as a subword so we are decoding it to get the original text. Comparing the 100.txt for ENglish we can see that the character level subword generates random word but those are not corelated to each water. Where for small vocab or larger vocab size the words generated are more sensible and it complements previous words. 

### OOV Comparison


### Conclusion

So what we have understand from doing the project is how we can use subword level embeddings for representing OOV words. We have analyzed 2 different language corpus and applied 3 level of subword granularity to each of them. After getting the subword corpora we trained a language model over it and generated some rnadom texts with the model. After comparing the generated words we understood that the vocabulary level subword contains more meaningful relations than character level subwords. We than consider original data as well as the genrated data to compare the OOV rates. 


