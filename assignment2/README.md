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

### Preprocessing Steps


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
