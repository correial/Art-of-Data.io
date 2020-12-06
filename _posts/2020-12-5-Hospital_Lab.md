--- 
#indicate Frontmatter
layout: post
title: Hospital Lab
---

# Which county has the most hospital beds per person?

New York contained the most hopsital beds per person
* The county contained a total of 7.14261 beds for every 1000 people!

<br>

# Discussion

_Discuss how you obtained and cleaned the dataset. Make sure to explain what methods you used and why._

**My Process**
1. I first figured out how to access the API by manipulating the base URL, the KEY, and the endpoint
2. I studied the format in which the API presented the data. I learned that each row of data (id) contained values and strings for different counties, bed types, populations, etc...
3. I generated a dictionary of all the values from the API through using a loop that would print each row in the data
4. After creating and printing this dictionary for every row of data, I piped what was printed into a csv file and stored it on my computer
5. I looked through the data and decided that the fastest approach would be to manually clean the dataset. I also believed that manually cleaning the data set would result in the fewest number of errors!
6. In order to clean the dataset I needed to chose a constant bed measure to ensure that the "beds per person" were consistent throughout the table
7. The file already contained the most "1000HAB" measures, and thus I converted the other measures into 1000. For each measure that was 500, I would multiply the "beds per person" value by two, then change the 500HAB to 1000HAB. I did the opposite for each 2000HAB, dividing the number of "beds per person" by two
8. I Then saved this file for later use in my "bed analyzation code" 


<br>

# Who did I work with?

During this lab, I collaborated a large about with Ben May and Ethan Waggoner! Ethan and I zoomed together late at night for hours discussing different methods for how to go about analyzing the cleaned csv file. However, after finilizing our pseudocode and testing out specific methods to access the file, we worked independently on the code for the most part. You may still see numerous overlaps in the concepts we used for our codes. Additionally, at one point, Ethan and I were stuck in figuring out how we could sort through the counties using two different lists. We went to Ben and he gave us suggestions and ideas of what our code could use.    

<br>

 # What methods I tried
 During this assingment, I tried numerous methods to sort through my csv file. Some worked, and even more didn't work at first. But through collaborating with classmates we finally figured it out! **Here are a few...**
 *  One thing to note about my program is that I essentially used two methods to find the county with the most beds just to ensure that I was recieving the correct answer! 
* One method that I used was a two dictionary method for keeping track of the county with the most beds as I ran through the rows. One dictionary held the county with the current maximum number of beds (cur_max). The other dictionary held the last county that was analyzed (cur_holder). If the "cur_holder" was ever greater than the "cur_max", then the county and number of beds in the "cur_holder" would replace the values of "cur_max". However, if the number of beds in the "cur_holder" was less than the "cur_max", the number of beds and county name for the "cur_holder" list would be reset. 
* As I ran through the rows of data I would also continously update the "total_beds" dictionary. This dictionary contained the total number of beds in each county. At the end of the program I printed this dictionary out. This allowed me to manually check to make sure that the county and bed number printed during my first method (above) was accurate!
* While both of these methods ended up working out in the end, I had a large about of trouble in the beginning. What was the most difficult for me was thinking of how I could add all of the beds in each county. However, using my "new_county" variable, I managed to figure out how to update each county as I ran through the rows in the data!

<br>

# What could have gone better
Honestly, I feel as though this lab went pretty well for me. Through collaboration I am now very proud of my finalized code! One thing that I would like to improve on is the use of more generalized variables throughout my code. While my program was not very hardcoded, I would like to see more integration of variables throughout the code so that my program could be used on other types of data and files.

<br>

# What I learned during this lab
I took away two major lessons from this lab:
1. I appreciate that through collaborating with others, there is never an assingment that can't be completed. While Ethan, Ben, and I are at similar levels in computer science, everyone has different approaches and thought processes. When we combined all of our ideas together, there was nothing missing from our code
2. As far as skills in computer science, I now feel comfortable creating a csv file from an API and how to clean data. It was very rewarding seeing my code compile after all of my work. **I look forward to the next lab!**

<br>

#### Written, Edited, Created, Thought of, and Programmed by: 
Lucca Correia (HM '22)  