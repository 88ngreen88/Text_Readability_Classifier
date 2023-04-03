### The Problem

Teachers, especially science and social studies teachers, are always looking for timely, grade appropriate texts for their students. Assessing the academic rigor and readability of a text can be a difficult task for teachers, despite being absolutely essential for student learning and engagement. While expensive sites like NEWSELA exist, their text corporas are often limited in their scope.

The model presented below gives teachers the opportunity to easily assess the readability of novel texts. The model will help support teachers in selecting the most grade appropriate reading for their class. In addition, the model can also be used by teachers in ICT classroom setting to differentiate novel texts for a diverse spectrum of learners. 

### Importing Data

I only used one data set to train my model. The data set I used is a text corpora that was created by Scott Crossley and his of research team at Georgia State University. Below I imported the text corpus and completed EDA on the corpus.

### Exploratory Data Analysis
Below I used pandas methods to explore the data set in order to answer the following questions about my data:

1. How large is the corpora
2. Are there any missing values in the corpora?
3. What is the range of years in which the texts were published?
4. Where did Georgia State University get the texts for this corpus?

<img width="585" alt="Screenshot 2023-04-03 at 7 10 09 AM" src="https://user-images.githubusercontent.com/115309980/229492943-4c0d50c7-41ff-4d02-a58e-36c3ff9e541d.png">

The information chart above shows that the corpus has 4724 rows with float, integer and object data types. While not huge, 4724 texts seems like enough data to appropriately trian my model. In addition, a few of the columns such as Anthology, Sub Cat, and License have null values. I am not concerned about the null values in theses columns because I do not needs these columns in order to create my model.

![download](https://user-images.githubusercontent.com/115309980/229493074-0acea2c8-cc83-4c17-985d-f0435b274aee.png)

Looking at the histogram above we can see that the publication dates occur in two tight clusters. These clusters of dates show that the majority of texts in my corpus were published either between 1850-1922 and 2010-2022. I believe that these clusters occur because most of texts are public domain texts or texts taken from sites like wikipedia.

In addition, the fact that a large number of the texts were published over 100 years ago creates a problem for my model. I was hoping that my model could be used to assess the readability of newer, novel texts. By training my model using a corpus that is so heavily skewed to older texts, my model may not be good at assessing the readability of newer texts.

Now that we have looked at the histogram of publication years, let's look at the authors who who, created the texts in my corpus:

<img width="387" alt="Screenshot 2023-04-03 at 7 11 38 AM" src="https://user-images.githubusercontent.com/115309980/229493199-edba0d7a-7d94-46ff-803f-7e5d281c6dec.png">

The value counts above shows that many of the texts were scraped from websites like wikipedia and USHistory.org. This is good for my model because looking at the list of authors above, many of the texts are from edcuational websites. Training my model on educational texts will probably improve my model's ability to accuraletly categorize novel educational texts.

In addition, 271 of the texts in this corpus are have unknown authors. For these values, the author is a question mark. Let's take a closer look at these texts in order to decide whether or not these rows should be taken out of the corpus.

<img width="883" alt="Screenshot 2023-04-03 at 7 12 21 AM" src="https://user-images.githubusercontent.com/115309980/229493332-0f6294ba-ad8e-46c8-ba9e-02419db53023.png">

Looking at the texts from unknown authors, most of the texts are from monthly publication where the authors are not specified. With this in mind, I will not drop these rows from my text corpus.

### Normalizing and Tokenizing Text (X - Value)
Now that I have visualed the data I will begin cleaning the text, which is in the column titled "Excerpt." I will clean the text by normalizing and tokenizing the words in the text in order to reduce the number of words in the corpus and prepare the data for NLP.

### Cleaning Readability Target Value (y - Value)
The corpus includes 11 different measures of readability: Lexile, BT Easiness Score, S.E., Flesch-Reading-Ease, Flesch-Kincaid-Grade-Level, Automated Readability Index, SMOG Readability, New Dale-Chall Readability Formula, CAREC,  CAREC_M, and CML2RI 

I first wanted to create a heatmap of these measures of readability to see how closely correlated all these values are to one another. 

![download-1](https://user-images.githubusercontent.com/115309980/229493682-1f540c7a-a7b5-4e49-bccb-e5df331148f7.png)

Looking at the heatmap above, I can see that all the measures of readability, the Flesch-Reading-Ease(FRE) score is the most correalted with the other scores. In addition, the FRE score is one of the most commonly used measures of readability along with the Lexile Band Score. 

I will make models using both the FRE Scores and the Lexile Band score in order to decide which target is best.

### Modeling

For my final model I used the xgboost classifier, which gave me a test accuracy of 77%

<img width="503" alt="Screenshot 2023-04-03 at 7 16 29 AM" src="https://user-images.githubusercontent.com/115309980/229494187-7a7f7762-336a-4df3-9d73-ce8f8e82c450.png">


![download-2](https://user-images.githubusercontent.com/115309980/229494190-01e9fafd-de18-431a-9bdc-8f9061371a6a.png)

### Conclusion

I would recommend that teachers EVENTUALLY use this model for the following:

1. Classify the readability of novel/new text
2. Get grade appropriate word recommendations for differentiating text

### Next Steps

In the next few days, I plan on implementing the following step in order to improve my model:

1. Scrape  more diverse texts to my corpus to better train my model especially for “Medium” texts. 
2. Feature engineer for authors and diagrams to add more “context” to my model
3. Find a better target for text readability scores
4. Run cosine similarity in order to create book recommendations


