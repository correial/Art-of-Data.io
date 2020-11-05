--- 
#indicate Frontmatter
layout: post
title: Postfix Calculator Lab
---



# Final Average 
_Calculate what each line in calculate_me.csv evaluates to. The only operators are +, -, and *! There is no /. What is the average of all the final values?_

* The average of all of the final values is ***529.91***

<br>

# Explain how a stack is used to evaluate postfix notation

In this lab, stack plays an integral part in evaluating postfix notation. As the program runs through the elements of the row, it will add them to a stack if they are an integer, not a symbol (-, +, *). Then when an element in a row is a symbol, the top two values of the stack will be popped off and either added, subtracted, or multiplied depending on what the symbol was. Then, the answer of that equation, whether it be addition, subtraction, or mulitplication will be pushed back onto the stack and the program will continue running through the elements of the row until it finds another symbol.

<br>

# Who did I work with?
The work in this lab is mine and mine only. However, at the beginning of the lab I brainstormed pseudocode with Ethan, and at the end of the lab I compared my final average with his.

<br>

# What methods you tried
* At the beginning of the lab I thought of a few methods for evaluating the postifx notation equations. My two main approaches were using an evaluate function to use within the "for row in data" loop. Or I could ignore using the method approach and complete the entire postfix notation evaluation within the "for row in data" loop. 
* I decided that it was more effective and clean to use an evaluate method and used pseudocode to map it out. I decided that I should use a stack to sort through the elements of the row. Then when the element in the row was a symbol (-, +, *), I would pop the top two values of off the stack and either multiply, add, or subtract them. I would then push this value back on the top of the stack
* I would return the top value of the stack when the loop reaches the end of the row by using the peek function
* Finally, I would use the evaluate function on the csv file by evaluating the row and using a variable to add keep track the number of rows. Then the average would be printed 

<br>

# What worked or didn’t work
* What worked: using an evaulate function and sorting through the row via use of a stack was very effective
* What didn't work: one of my original plans of using a list and appending values to it did not work, and thus I switched to using a stack

<br>

# What I learned during this lab. 
* During this lab, I made an effort to keep my code as clean and general as possible. I did this by creating an evaluate function and using it to evaluate the csv file provided. Moreover, I learned the benefits that come with using a general function rather than hardcoding methods within the "for row in data" loop.

<br>


### Written, Edited, Created, Thought Of, and Programmed by: 
Lucca Correia (HM '22)   




