## Preprocessing Steps / How to Run the File 

 

## Question 1: Positional Index  

### Methodology  

1. The first part of this question was to do the preprocessing tasks on the dataset.
   
    *  We read the files from the directory and performed our preprocessing function on them.  

    * Preprocessing function:   

        * Convert to lowercase text, remove special characters (such as punctuations, special characters, etc.), perform word tokenization, remove stop words, and eliminate empty strings  

        * After fixing the above criteria we created a dictionary which includes the location of each word in the file  

        * This function returns two dictionaries – one with the names of the files and the other with all the words in the files and their position in the corresponding file.  


2. The second part of this question we had to develop the data structure. To do this we created different classes.  

    * Created a Linked List class which can insert, print, and merge the values (document IDs, frequency, and list of positions). This is used to store the positions of the words.  

    * Created a Positional Index class which inserts, retrieves the specific value (word with the position list), and can retrieve the linked list of positions for a specific document ID  

    * Used the Hash Inverted Index class from previous Assignment which we can set the index, insert the key value pair (word, docID), and retrieve a set of values for a given key.
      

3. The next part was to allow the user to type a query and output the required results. To do this we created functions.  

    * Created a function to find the common documents from the query. This uses the Inverted Index that is returned from the Hash Class. We retrieve the documents for the words from the query and take the intersection to find where all the words from the user entered query occur in all the documents.  

    * Created a function to return all the positions in a specific document in which the positions are in the same order / next to as the user’s query. This uses the Positional Index returned from the Positional Index class. We retrieve all the documents with that specific word and the positions in which it is found, as a dictionary. Since we care about the positions we focused on the linked list values. We decided to see if the words were following each other, to shift the words so they are all the same value. Since we could set the positions as the same value, we could use the intersection function again to take the positions which are the same for every word. We then took out our adjustments and returned the final list of the starting positions for the query.  

  
4. The final part was to put everything together.  

    * We can ask the user to input a string, with the criteria that once the preprocessing steps run, the query is less than 5 words. We also verify this is the case otherwise we will ask the user to enter another string.  

    * Once they enter the correct query and there are still values in the string (after the preprocessing steps run), we run all the functions we created (to find the common documents and positions) and display the results.  

    
### Assumptions  

For this question we made a few assumptions:  

  * We assumed to get the positions after all the preprocessing, this way if the user were to enter a string “pyramid and scheme” we will return anywhere that “pyramid” and “scheme” are next to each other.
    
  * We also assumed the user can enter as many words / non words as possible and we check the criteria that it is less than 5 words after the user-entered string gets preprocessed.  


### Description of Outputs and Analysis Conducted  

In the final chunk of code for this question we output the following:  

* Every time the user enters a sentence and after the preprocessing steps have been applied. This can be repeated until the user enters a string that matches the criteria.
    
* The file name for which the position of the query matches the position in the file  

* The query starting position. This is the position in which the first word of the user entered query is found in the text file followed by the rest of the words in the user’s query.  

* The number of matching documents  

* And finally, a list view for all the files where the user’s query is found in the order.  


## Question 2 - TF-IDF


### Methodology

1. To begin this question, we applied the pre-processing steps from question 1.  

2. Next, we created an empty matrix that would later become our TF-IDF Matrix. 

* We set the dimensions of this matrix to have the number of rows equal the number of total documents. The number of columns equals the total number of words in all documents which we found through the positional index. 

3. To populate the TF-IDF values in the matrix for each word in the vocabulary, we started by creating a function to apply the five different weighting schemes to calculate the term frequency. 

* Binary (weight = 1): This tells us whether a word exists in a document or not. To calculate the term frequency we use the positional index dictionary to find the list of documents that contains the word. If the document ID is found in the dictionary, tf is set to 1, otherwise it is set to 0 meaning the word was not found in the document. 

* Raw count (weight = 2): The raw count is the number of times a word appears in a document. To calculate the term frequency we use the positional index dictionary to find the list of documents that contains the word. If the document ID is found in the dictionary we take the value of the key, value pair which gives us the frequency of the word in that document. 

* Term Frequency (weight = 3): This is the frequency of the word divided by the sum the frequencies of all other unique terms t′ in the document d, excluding the term t. To calculate the term frequency we take the raw count and divide that by the number of unique words found in the document subtracting 1 by using the position_words dictionary. 

* Log Normalization (weight = 4): This is the log of the term frequency of the word in the document plus 1. To calculate this we take the log of the raw count + 1. 

* Double Normalization (weight = 5): For this we need to find the highest term frequency in the document  (the number of the word that appears the most). To find this we loop through the position_words dictionary to and determine the frequency of each word in a document to determine the maximum number. We then take that value and the raw count and apply the formula: 0.5 + (0.5 x (raw_count / max)). 

4. The query vector was created to determine whether the term exists in the current vocabulary list. If the word in the query is found in the vocabulary list, it will be flagged with a 1, but if it is not found the value will remain 0. 

5. To calculate the TF-IDF score, we created a function called calc_tfidf which uses the formula IDF(word) = log(total number of documents / (document frequency (word) + 1)). From here this IDF value was multiplied by the TF-IDF value given by the weighting function. Another function called tf_idf_vals is called to aid in populating the TF-IDF Matrix. This function calls the tf_idf_matrix function to build a matrix with the number of rows being the number of documents, and the number of columns being the number of words in all documents. This function loops through the documents we have, as well as all words in the vocabulary list, and proceeds to call the calc_tfidf function. We then populate the matrix for the current document and word index with the calculated TF-IDF score. 

Now using the TF-IDF Matrix we determine the top 5 relevant documents. We created a dictionary to help us store the key value pairs (docID and similarity score). We looped through the current TF-IDF Matrix to calculate the dot product using the query vector and each row in the matrix (which represents each document). Once all the dot product values were stored in the dictionary, we sorted by the values in descending order and indexed the top 5 to return the top 5 relevant documents. 

6. To apply the 5 different weighting schemes for term frequency calculation, we allow user input of the query (up to 5 words) and their chosen weighting scheme (from 1-5). This will result in the tf_idf_matrix function to build the matrix and the tf_idf_vals function to populate the TF-IDF Matrix  with the TF-IDF scores in terms of the query and weighting scheme. This will result in the top 5 relevant documents and their respective TF-IDF scores. 

### Assumptions


### Description of Outputs and Analysis Conducted

## Question 3 - Cosine Similarity

### Methodology 

 For this function we called the query vector and the term frequency inverted document frequency matrix from question 2.  

1. The formula for calculating cosine similarity is Cosine Similarity = (A . B) / (||A|| * ||B||)  

  * Where A represents the matrix for the query vector and B represents the matrix which includes the weights.  

  * Take the dot product of these values and divide by the product of each individual Euclidean distance  

2. Created a dictionary to set the document ID to the correct score from the formula 

3. Created an array to get the top 5 documents for this method and return this 

4. Using the user inputs from question 2 we call the cosine similarity function and return the corresponding documents 

 

### Assumptions 

 For this question, we assumed that the Term Frequency will be run first before calling the Cosine Similarity function. 

  

### Description of Outputs and Analysis Conducted 

In the final chunk of code for this question we output the following:  
 
  * Top 5 cosine list:
    
     * with the document ID and the cosine similarity scores that correspond to the files
       
     * with document names and the cosine similarity scores that correspond to the files
   
 ### For each scoring scheme, provide a report stating the pros and cons of using that particular scheme to determine document relevance. 

## Binary 

Pros:  

* Simple calculation  

* Quicker processing time 

Cons: 

* TF-IDF score may not be as accurate as other schemes as we only use either 0 or 1 as the tf 

## Raw Count 

Pros: 

* Simple calculation 

* Uses the actual frequency of the terms in a document 

Cons: 

* Score may be skewed due to document length 

## Term Frequency 

Pros: 

* Normalizes the scores by considering the number of words in the document 

Cons: 

* Takes a longer time to process as it must find all the terms in the documents 

## Log Normalization 

Pros: 

* Simple calculation 

* Reduces impact of high term frequency, so very common terms do not dominate 

Cons: 

* Log values may not be easily interpreted 

## Double Normalization 

Pros: 

* Normalizes term frequency relative to the most frequent term so document size does not have as much impact 

Cons: 

* Takes longer time to process as it must find all the terms in the document and keep track of the highest frequency 

* More complex calculation 
