# Text Retrieval and Search Engine (CP423)
### Assignment 2 - Group 5
### Group Members:
* Abigail Lee
* Kayleigh Habib
* Myisha Chaudhry
 

## Preprocessing Steps / How to Run the File 

Run all the code in the order it appears. 

 

## Question 1: Webscraping  

### Methodology  

1. Part 1-3 was to retrieve the webpage, decode it into a tree structure and get the tables we are interested in 

    * To do this we utilized the ‘requests’ library and ‘BeautifulSoup’ library. The request library was used to get the raw HTML of the webpage, while the BeautifulSoup library was used to help get our data into a tree structure and to find all the tables. 

2. Part 4 was to merge the tables and sanitize into a single dictionary 

    * To do this we first created a sanitize function to help clean the data, so that when we merge the data there will be no repeated rows (province names). 

    * We then went through our list of tables, calling the Pandas ‘read_html’ function which creates a DataFrame, we then converted the table to a string and called our sanitize function on the data. 

    * We then merged the data using an outer join as the province names was a common field in all the tables. 

    * We converted these dataframe to a dictionary and sanitized all the data again 

3. Part 5 was to convert the dictionary into a dataframe 

    * To do this we called the Pandas DataFrame function and inputted the dictionary from the previous question 

4. Part 6 was to locate all h2 elements on the HTML page and display their text content 

    * To do this we used the find_all method in the BeautifulSoup library to search for and retrieve all the occurrences of headers (h2) in the webpage. 

    * We then looped through the elements and pulled the text content using get_text 

    * We then removed the ‘[edit]’ text from the headers 

5. Part 7 was to generate a list of all hyperlinks embedded within the table 

    * To do this we used the find_all method in the BeautifulSoup method to search for and retrieve all the <a>, which contain the hyperlink elements in the inter_tables list 

    * We then looped through each hyperlink found and got the href attributes and title attributes which contains the URL elements 

    * Then we checked if the href existed and if it was a valid Wikipedia link and constructed the full URLs by combining the href with the base URL, ‘https://en.wikipedia.org’ 

    * Then we appended the full URLs to the hyperlinks list and the titles to the title list 

6. Part 8 was to download every webpage from the links in the previous step 

    * To do this we created a folder called “webpages” that would store all the webpages from the links 

    * We got the content from each page and created an html file for the various pages. We used the “names” array from the previous part, to name our html files.  

    * We then wrote out the content to the corresponding html file 

 

### Assumptions  

In this assignment we assumed this was the only link to be used and we are interested in all the tables in this link for part 3.  


### Description of Outputs and Analysis Conducted  

Below are our following outputs and snapshots of outputs 

Part 1: String output of the raw HTML 
![Screenshot 2024-07-06 at 4 03 50 PM](https://github.com/kayl26/TextRetrieval_SearchEngines/assets/98178120/86d136d0-09e0-448c-bdce-af43faae94cb)

Part 2: Raw HTML in tree structure  
![Screenshot 2024-07-06 at 4 04 09 PM](https://github.com/kayl26/TextRetrieval_SearchEngines/assets/98178120/31149c84-f11c-4714-84d3-324d87343305)

Part 3: List of the raw HTML for the tables 
![Screenshot 2024-07-06 at 4 04 37 PM](https://github.com/kayl26/TextRetrieval_SearchEngines/assets/98178120/2647ab8e-93d2-4b5e-a418-a74bb9f6153d)

Part 4: Dictionary of the tables. This is a dictionary inside a dictionary where {column names: {index: data values}, ....} 
![Screenshot 2024-07-06 at 4 04 57 PM](https://github.com/kayl26/TextRetrieval_SearchEngines/assets/98178120/b5c6b703-e697-4fc0-92a1-53c79e03a203)

Part 5: Pandas dataframe of the merged and sanitized tables from the dictionary above 
![Screenshot 2024-07-06 at 4 05 23 PM](https://github.com/kayl26/TextRetrieval_SearchEngines/assets/98178120/5b2c30a1-866d-4383-be0e-9edef8f22c1d)

Part 6: The secondary headers (h2) from the webpage 

![Screenshot 2024-07-06 at 4 05 39 PM](https://github.com/kayl26/TextRetrieval_SearchEngines/assets/98178120/cea22813-78c3-4f70-8bc1-8f7130c58e0d)

Part 7: List of the hyperlinks 
![Screenshot 2024-07-06 at 4 05 59 PM](https://github.com/kayl26/TextRetrieval_SearchEngines/assets/98178120/a522ade8-c954-4b54-9fa2-0f4551bd3e39)

Part 8: Folder for the downloaded webpages 

![Screenshot 2024-07-06 at 4 03 17 PM](https://github.com/kayl26/TextRetrieval_SearchEngines/assets/98178120/77a8602d-d84b-408a-84fc-664acbca9fb0)

 
