---
layout: post
title: Physical Health Lab
---

4

# Which dataset did you work with?

***I analyzed a csv file generated from a survey conducted on HM students regarding their physical health in-person vs. online school*** 


# Dataset Analyzation

### Analyze where it’s from
As mentioned above, the CSV was generated from the responses of a survey. This survey is part of a research project that examines Horace Mann (HM) 9th through 11th grade variation in student physical Health between in-person and online school for the 2020-2021 school year.

### What assumptions does the dataset make:
 The two major assumptions that the data set makes are an accurate representation of the population and correct responses. 
 1) The sample size of the data set contained 135 student responses with a proportional response rate from each grade. Our team agreed that the magnitude of responses was large enough to assume they accurately and holistically represented the population of all 9th-11th graders at HM. 
 2) The second assumption made is that all responses are accurate and indicative of a student's actual life. While there is no method of guaranteeing that this is true, our team reduced any confusion and need for question interpretation as all answers were multiple choice and concise. 


### What data might be missing?
The majority of survey questions focused on areas of physical health where answers would consist of quantitative values. While this subset of questions enables more efficient data cleaning and a reduction in bias responses, it leaves a significant aspect of understanding a student's physical health: why? Our responses lacked student reasoning and motivations behind their answers. Thus the focus on straightforward quantitative questions came at the price of a holistic understanding of a student's physical health


### Dataset biases 
- As stated above, most survey questions yielded quantitative answers, thus there was minimal bias surrounding the interpretation of questions. Additionally, the quantitative multiple choice answers curbed the effects of personal bias and perspectives such as what it means to be stressed. 
- However, throughout the survey, students were asked the make large generalizations about categories for physical health such as the average hours of sleep per night during online school. These generalizations may not encompass a student's authentic sleep schedule. Thus the dataset may be prone to bias relating to student's view of how to calculate "average hours of sleep" if their hours of nightly sleep greatly alter from a night to night basis.


### Null and alternative hypotheses
* My alternative hypothesis is that students receive more sleep during online than in in-person school. 
* My null hypothesis is that the work environment does not affect on average hours of nightly sleep

<br>

# Variable Descriptions and Analysis

![.]({{ site.baseurl}}/assets/img/denseedit.png)

**Code for this graph:**
```
alt.Chart(Health).transform_density(
    'Online Sleep',
    as_=['Online Sleep', 'density'],
).mark_area(opacity = .5).encode(
    x=alt.X('Online Sleep:Q', title="Hours of Sleep"),
    y='density:Q',
) + alt.Chart(Health).transform_density(
    'In-person Sleep',
    as_=['In-person Sleep', 'density'],
    bandwidth = .65,
).mark_area(color="red", opacity = .5).encode(
    x="In-person Sleep:Q",
    y='density:Q',
).properties(
    title = "Online Sleep vs In-Person Sleep",
)
```

<br>

### Online Sleep Varaible Table (Blue Graph)
**Code used to obtain these statistics:** `Health["Online Sleep"].describe()`

| | Count | Mean | Max | Standard Deviation | Median | Skew | 
| :------ |:--- | :--- | :--- | :--- | :--- | :--- |
| **Value** | 136.000000 | 7.507353 | 10.500000 | 1.201828 | 7.500000 | N/A |
| **Meaning** | 136 students answered this question on the survey | This tells us that the average nightly hours of sleep during online school is roughly 7.5 hours| The maximum hours of sleep a student received during online school 10.5 hours | There was very minimal variance in the data/histogram | The graph is centered around 7.5 hours | This graph experiences very little skew; it is almost perfectly symmetrical |

<br>

### In-Person Sleep Variable Table (Red graph)
**Code used to obtain these statistics:** `Health["In-person Sleep"].describe()`

| | Count | Mean | Max | Standard Deviation | Median | Skew | 
| :------ |:--- | :--- | :--- | :--- | :--- | :--- |
| **Value** | 136.000000 | 6.613971 | 9.500000 | 1.086903 | 6.500000 | N/A |
| **Meaning** | 136 students answered this question on the survey | This tells us that the average nightly hours of sleep during online school is roughly 6.6 hours | The maximum hours of sleep a student received during online school 9.5 hours | There was very minimal variance in the data/histogram | The graph is centered around 6.5 hours | the red graph skews slightly to the right, however, remains symmetrical for the most part |

<br><br>
--

# Exploratory Visualization

![.]({{ site.baseurl}}/assets/img/picture.png)
**Code for this graph:**
```
New_data = []

with open("Art of Data Lab 2 - Sheet1.csv", "r") as f: 
    data = csv.DictReader(f) 
    for row in data: 
        In_Person_Record = {"Grade": row["Grade"], "Hours": float(row["In-person Sleep"]), "Online?": False}
        Online_Record = {"Grade": row["Grade"], "Hours": float(row["Online Sleep"]), "Online?": True}
        New_data.append(In_Person_Record)
        New_data.append(Online_Record)
       
df = pd.DataFrame(New_data)

sns.violinplot(data=df, x="Grade", y="Hours", hue="Online?", split=True, inner="quartile", palette="Set2").set(title='Online vs. In-Person Sleep Comparison', ylabel = "Hours of Sleep")
```
<br>

### What we learn from the exploratory violin graph
* The line with the longest dashes represents the median (there is one for each grade and school environment). From the violin plot, we see that this line remains level among grades, however changes based on the environment (in person or online). 
    * For in-person sleep (green), the median hours of sleep is approximately 6.5. This is the number we expected since it does not change as a function of grades, and thus should match the median hours of in-person sleep for the data set which was calculated in the table above
    * For online sleep (orange), median hours lie around 7.5 hours for all grades. This also makes sense as it matches the online sleep median in the table above
* This exploratory graph is evidence to explore that there may be a relationship between hours of sleep and the school environment. Bootstrapping and p-value calculations will be conducted for further confidence and confirmation.

<br>
---

# Bootstrapping: Online Sleep

**Bootstrapping Code:** 
```
def bootstrap_sample(z):
  boot_sample=z.sample(136,replace=True)
  return (boot_sample).mean()

def bootstrap_samples(N,x):
  holder=[]
  for i in range (0,N):
    holder.append(bootstrap_sample(x))
  return holder

z=Health['Online Sleep']
Online_data = pd.DataFrame(bootstrap_samples(5000,z))

print(Online_data.describe())
```

<br>

### Generated Distribution After Bootstrapping

![.]({{ site.baseurl}}/assets/img/onhist.png)


As expected, the mean, median, and max of the bootstrap sample (run 5,000 times) remain consistent with the original dataset. However, the standard deviation after bootstrapping is 0.103366 (instead of 1.201828). This is further evidence that the data in the original dataset for online sleep contains little skew and overall deviation. 


### Confidence Intervals
**Code Used:**
```
print(Online_data.quantile(.025))
print(Online_data.quantile(.975))
```

The calculates 95% confidence interval is 7.301471 to 7.705882 hours of sleep for online school. This means that our team can be 95% confident that online sleep hours for students will lie between 7.301471 and 7.705882. This interval will be compared to in-person sleep confidence intervals later on

<br>
---

# Bootstrapping: In-person Sleep

## Bootstrapping Code 
```
def bootstrap_sample(z):
  boot_sample=z.sample(136,replace=True)
  return (boot_sample).mean()

def bootstrap_samples(N,x):
  holder=[]
  for i in range (0,N):
    holder.append(bootstrap_sample(x))
  return holder

z=Health['In-person Sleep']
In_person_data = pd.DataFrame(bootstrap_samples(5000,z))

print(In_person_data.describe())
```
## Generated Distribution After Bootstrapping
![.]({{ site.baseurl}}/assets/img/inhist.png)


Similar to online sleep, the mean, median, and max of the bootstrap sample (run 5,000 times) remain consistent with the original dataset for in-person sleep. However, the standard deviation after bootstrapping is 0.092000 (instead of 1.086903). This is further evidence that the data in the original dataset for online sleep contains little skew and overall deviation. 

<br>

## Confidence Intervals
**Code Used:**
```
print(In_person_data.quantile(.025))
print(In_person_data.quantile(.975))
```

The calculated 95% confidence interval is 6.441176 to 6.801471 hours of sleep for in-person school. This means that our team can be 95% confident that in-person nightly hours of sleep for students will lie between 6.441176 and 6.801471. When comparing this data to the online sleep interval, we can now conclude, with 95% confidence, that students during online school receive roughly an hour more of sleep every night. This upholds my hypothesis that HM students receive more sleep during online than in in-person school. The final step to confirm this trend is statistical significance testing.

<br>
---

# Statistical Significance: the P-value
**Code Used:**
```
sorted_ls = sorted(Online_data)
P_num = 0

for i in sorted_ls:
  if i >= In_person_df:
    P_num += 1
   
print(P_num/(len(sorted_ls)))
```

***P-Value: 0.0***

* The P value, for this code, is simply the percent probability of a value in the Online-sleep data being greater than or equal to the average In-person sleep data. If we look at our distribution above, we see that there are no such values, and thus "P_num" remains at 0, and 0 divided by anything is 0! With this result, we can safely reject the null hypothesis and confirm that the data upholds the alternative hypothesis: students recieve more hours of nightly average sleep during online school than in-person school!

<br>

## Written, Edited, Created, Thought of, and Programmed by: 
***Lucca Correia (HM '22)***  
Thank You Mr. Lee for a truly unforgettable year!!