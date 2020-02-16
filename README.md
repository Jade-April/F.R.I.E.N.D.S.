<img src='top.PNG' alt="Italian Trulli" style="width:300px;height:200px;">

<h2>What is it?</h2>
<p><strong>The project is aimed to establish a recommendation system taking advantage of Twitter API to help users find the most ideal and suitable friends of themselves. </strong>
<li><b>Assumption:</b> Network (real life distance), interest, personality, location are the most influential factors of friendship. Personality and location choices are personal preference whereas network and interest yield to computer calculation.
<li><b>Assumption Basis:</b> Psychological study, intuition, available data from Twitter

<h2>Main features</h2>
Here is how the system works:
<p>
  <li><strong>Layer I of recommender system: MBTI personality</strong>
  <p>Based on our assumption, personality is another dark matter of friendship. People tend to be more comfortable with some special types of personality, or they may be attracted with people with opposite personality. Thus, it is hard to determine which one is better, so it is also a subjective area left for personal choice.</p>
  <p>In this part, we classified users in our dataset to 16 MBTI personality types according to the content of their tweets with Python library FastAI. We tuned the pretrained NLP model AWD_LSTM to serve our goal. Our training dataset is downloaded from Kaggle. Our reference: https://www.myersbriggs.org/my-mbti-personality-type/mbti-basics/the-16-mbtitypes.htm?bhcp=1
<p>
<li><strong>Layer Ⅱ of recommender system: Recommendation Based on Machine Learning</strong>
  <p><b>Common following [interest]:</b> First, we found out that following (A→B) indicates user A’s interest. Therefore, we constructed the feature “common following” by counting the number of common following. Second, we further found that some users have a long following list so he/she tends to have more common following in most cases. To eliminate the scale factor, we standardized our feature: 𝑐𝑜𝑚𝑚𝑜𝑛 𝑓𝑜𝑙𝑙𝑜𝑤𝑖𝑛𝑔 √𝑓𝑜𝑙𝑙𝑜𝑤𝑖𝑛𝑔𝑢𝑠𝑒𝑟1× 𝑓𝑜𝑙𝑙𝑜𝑤𝑖𝑛𝑔𝑢𝑠𝑒𝑟2 . Finally, to avoid the denominator from being 0 (invalid), we adjusted it to 𝑐𝑜𝑚𝑚𝑜𝑛 𝑓𝑜𝑙𝑙𝑜𝑤𝑖𝑛𝑔 √(𝑓𝑜𝑙𝑙𝑜𝑤𝑖𝑛𝑔𝑢𝑠𝑒𝑟1+1)×(𝑓𝑜𝑙𝑙𝑜𝑤𝑖𝑛𝑔𝑢𝑠𝑒𝑟2+1) . (* In our dataset, we don’t need to worry about this because all our users have at least one following – Columbia University. But to ensure our method to be more applicable, we still make this adjustment.)
  <p><b>Distance [network]:</b> Instead of one-way following, 2-way following can indicates real-life friendship. Thus, we built the feature “distance”. The problem was that some users don’t have any path between each other, then the distance should be infinity which would cause error. To solve this, we chose 10,000 to represent infinity. It was found that distance in our dataset can be at most 2, thus we believe that 10,000 is big enough. 
  <p><b>Similarity [interest]:</b> LSI measures the similarity in words and topics, which can measure similarity in interest. All other users’ tweets (all users except A) are inputted as dictionary and corpus, then input A’s tweets to output the similarity with other users</p>
    <p>We tried Decision Tree, Random Forest, Bagging on our dataset using GridSearchCV to find the best parameter. Finally we chose Random Forest because it has best performance.  
<p>
  <li><strong>Bonus 1: Personal Topic Analysis</strong>
  <p>Based on tweets she/he has posted before; we try to find a pattern and deduce the TOP 3 TOPICS a specific user focuses on in his/her daily life so as to clarify target use’s interests and complete the match more efficiently. We can even provide them with some insights on what topic they might both be interested in when creating the first conversation. 
<p>
  <li><strong>Bonus 2: Emoji</strong>
  <p>We used Demoji package to accurately find or remove emojis from a blob of text. We select top 50 emojis of each person and generate common emoji with the recommended friends. 
<p>
<h2>Where to get it?</h2>
<p>This application can be found at https://tools-for-analytics-254001.appspot.com.

<h2>Dependencies</h2>
<p>To use this application, you can just click the links above and no dependency is needed. </p>
<p>However, if you want to run this application in your local ip address, see the <a href='https://github.com/Jade-April/Project-Group-16/blob/master/requirements.txt'>requirements.txt</a> for minimum supported versions of required dependencies.
