# Project---Part-1-Sentiment-Classifier
#We have provided some synthetic (fake, semi-randomly generated) twitter data in a csv file named project_twitter_data.csv which has the text of a tweet, the number of retweets of that tweet, and the number of replies to that tweet. We have also words that express positive sentiment and negative sentiment, in the files positive_words.txt and negative_words.txt.

Your task is to build a sentiment classifier, which will detect how positive or negative each tweet is. You will create a csv file, which contains columns for the Number of Retweets, Number of Replies, Positive Score (which is how many happy words are in the tweet), Negative Score (which is how many angry words are in the tweet), and the Net Score for each tweet. At the end, you upload the csv file to Excel or Google Sheets, and produce a graph of the Net Score vs Number of Retweets.

To start, define a function called strip_punctuation which takes one parameter, a string which represents a word, and removes characters considered punctuation from everywhere in the word. (Hint: remember the .replace() method for strings.)














punctuation_chars = ["'", '"', ",", ".", "!", ":", ";", '#', '@']
def strip_punctuation(word):
    new_word = ""
    print("word is: ", word)
    for char in word:
        if char not in punctuation_chars:
            new_word = new_word + char
    return new_word

def get_pos(sentence):
    str1 = sentence.split()
    print("string------", str1)
    wrd_cnt = 0
    for word in str1:
        if word in positive_words:
            wrd_cnt = wrd_cnt + 1
    return wrd_cnt
positive_words = []
print(type(positive_words))
with open("positive_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ';' and lin[0] != '\n':
            positive_words.append(lin.strip())
word_list = """#incredible You are a beautiful, wonderful person. I enjoy your company, and you are a delight
to all who know you. today! I am happy I met you. You accumen is good, great perfect and all that."""

clean_list = strip_punctuation(word_list)
print(clean_list)

pos_cnt = get_pos(clean_list)
print(pos_cnt)










#Next, copy in your strip_punctuation function and define a function called get_pos which takes one parameter, a string which represents a one or more sentences, and calculates how many words in the string are considered positive words. Use the list, positive_words to determine what words will count as positive. The function should return a positive integer - how many occurances there are of positive words in the text.







punctuation_chars = ["'", '"', ",", ".", "!", ":", ";", '#', '@']
positive_words = []
with open("positive_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ';' and lin[0] != '\n':
            positive_words.append(lin.strip()) 
    def get_pos(one_word):
        count=0
        one_word=one_word.split(" ")
        for word in one_word:
            if word in positive_words:
                count+=1
        return count
        
            
            




#Next, copy in your strip_punctuation function and define a function called get_neg which takes one parameter, a string which represents a one or more sentences, and calculates how many words in the string are considered negative words. Use the list, negative_words to determine what words will count as negative. The function should return a positive integer - how many occurances there are of negative words in the text.




punctuation_chars = ["'", '"', ",", ".", "!", ":", ";", '#', '@']

negative_words = []
with open("negative_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ';' and lin[0] != '\n':
            negative_words.append(lin.strip())
            
    def get_neg(one_word):
        count=0
        one_word=one_word.split(" ")
        for word in one_word:
            if word in negative_words:
                count+=1
        
        return count








Finally, copy in your previous functions and write code that opens the file project_twitter_data.csv which has the fake generated twitter data (the text of a tweet, the number of retweets of that tweet, and the number of replies to that tweet). Your task is to build a sentiment classifier, which will detect how positive or negative each tweet is. Copy the code from the code windows above, and put that in the top of this code window. Now, you will write code to create a csv file called resulting_data.csv, which contains the Number of Retweets, Number of Replies, Positive Score (which is how many happy words are in the tweet), Negative Score (which is how many angry words are in the tweet), and the Net Score (how positive or negative the text is overall) for each tweet. The file should have those headers in that order. Remember that there is another component to this project. You will upload the csv file to Excel or Google Sheets and produce a graph of the Net Score vs Number of Retweets. Check Coursera for that portion of the assignment, if you’re accessing this textbook from Coursera.






punctuation_chars = ["'", '"', ",", ".", "!", ":", ";", '#', '@']
positive_words = []
with open("positive_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ';' and lin[0] != '\n':
            positive_words.append(lin.strip())
negative_words = []
with open("negative_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ';' and lin[0] != '\n':
            negative_words.append(lin.strip())

negative_words = []
with open("negative_words.txt") as pos_f:
    for lin in pos_f:
        if lin[0] != ';' and lin[0] != '\n':
            negative_words.append(lin.strip())

def strip_punctuation(x):
    for char in punctuation_chars:
        x = x.replace(char, "")
    return x  

def get_pos(y):
    pos = 0
    y_strip = strip_punctuation(y)
    list_pos = y_strip.split()
    for w in list_pos:
        if w in positive_words:
            pos = pos + 1
    return pos

def get_neg(z):
    neg = 0
    z_strip = strip_punctuation(z)
    list_neg = z_strip.split()
    for w in list_neg:
        if w in negative_words:
            neg = neg + 1
    return neg

twitter_data = open('project_twitter_data.csv','r') 
twitter_data_lines = twitter_data.readlines()
print(twitter_data_lines)

twitter_sentiment = open("resulting_data.csv", "w")
twitter_sentiment.write('Number of Retweets, Number of Replies, Positive Score, Negative Score, Net Score')
twitter_sentiment.write('\n')
for line in twitter_data_lines[1:]:
    #Number_of_Retweets = line[-4]
    #Number_of_Replies = line[-2]
    Positive_score = get_pos(line)
    Negative_score = get_neg(line)
    Net_score = get_pos(line) - get_neg(line)
    row_string = '{}, {}, {}, {}, {}'.format('Number_of_Retweets','Number_of_Replies',Positive_score,Negative_score,Net_score)
    twitter_sentiment.write(row_string)
    twitter_sentiment.write('\n')
twitter_sentiment.close()
