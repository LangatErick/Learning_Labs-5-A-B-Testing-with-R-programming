# Learning_Labs-5-A-B-Testing-with-R-programming
* Split testing * is another name for A/B testing and it’s a common or general methodology. It’s used online when one wants to test a new feature or a product. The main agenda over here is to design an experiment that gives repeatable results and is robust enough to make an informed decision to launch it or not. Generally, this test includes a comparison of two web pages by representing variants A and B for them, as the number of visitors is similar the conversion rate given by the variant becomes better. Overall, it’s an experiment where two or more variations of the same web page are compared together by showcasing them to real-time visitors, determining which one performs better for a given goal. A/B testing is not only used or limited by web pages only, it can be used in emails, popups, sign-up forms, apps, and more. Let’s look into the example of a case study. So let’s implement AB testing in the R language.

## Case Study
Let’s imagine we have results of A/B tests from two hotel booking websites, (Note: the data is not the real one ). First, we need to conduct a test analysis of the data; second, we need to conclude the data we obtained from the first step, and in the final step, we make recommendations or suggestions to the product or management teams.

## Data Set Summary

- Variant A is from the control group that tells the existing website features or products.
- Variant B is from the experimental group to check the new version of a feature or product to see if users like it or if it increases conversions(bookings).
- Converted is based on the data set given, there are two categories defined by logical value. It’s going to show true when the customer completes bookings and it’s going to show false when the customer visits the sites but not makes a booking.
## Test Hypothesis
- Null Hypothesis: Both versions A and B have an equal probability of conversion or driving customer booking. In other words, there is no difference or no effect between A and B versions
- Alternative Hypothesis: Versions both A and B possess different probabilities of conversion or driving customer booking and there is a difference between A and B versions. Version B is better than version A in driving customer bookings. PExp_B! = Pcont_A.
Analysis in R
![image](https://github.com/LangatErick/Learning_Labs-5-A-B-Testing-with-R-programming/assets/124883947/12cccc21-c19e-4c6c-8a87-0ab940c5e5fe)

## Recommendation & Conclusions
Variant A has 20 conversions and 721 hits whereas Variant B has 37 conversions and 730 hits.
Relative uplift of 82.72% based on a variant A conversion rate is 2.77% and for B is 5.07%. Hence, variant B is better than A by 82.72%.
For this analysis P-value computed was 0.02448. Hence, there is strong statistical significance in test results.
The above results depict strong statistical significance. You should reject the null hypothesis and proceed with the launch.
Therefore, Accept Variant B, and you can roll it to the users for 100%.

## Limitations
It is one of the tools for conversion optimization but it’s not an independent solution it’s not going to fix all our conversion issues and it can’t fix the issues as you get with messy data and you need to perform more than just an A/B test to improve on conversions. 
---
title: "A/B Testing/Split Testing in R Programming"
author: "@erick"
format: docx
---

### A/B Testing/Split Testing in R Programming

#### AB Testing With R Programming

Split testing is another name of A/B testing and it\'s a common or general methodology. It\'s used online when one wants to test a new feature or a product. The main agenda over here is to design an experiment that gives repeatable results and robust to make an informed decision to launch it or not. Generally, this test includes a comparison of two web pages by representing variants A and B for them, as the number of visitors is similar the conversion rate given by the variant becomes better. Overall, it\'s an experiment where two or more variations of the same web page are compared against together by showcasing them to real-time visitors, and through that determines which one performs better for a given goal. A/B testing is not only used or limited by web pages only, it can be used in emails, popups, sign-up forms, apps, and more. Let\'slook into the example of a case study. So let\'s implement AB testing in the [**R language**](https://www.geeksforgeeks.org/introduction-to-r-programming-language/).

#### Case Study

Let\'s imagine we have results of A/B tests from two hotel booking websites, (Note: the data is not the real one ). First, **we need to conduct a test analysis of the data**; second, **we need to draw conclusions from the data** which we obtained from the first step, and in the final step, **we make recommendations or suggestions to the product or management teams.**

### Data Set Summary

Download the data set from[ **here**](https://github.com/etomaa/A-B-Testing/tree/master/data).

-   Variant A is from the control group which tells the existing features or products on a website.

-   Variant B is from the experimental group to check the new version of a feature or product to see if users like it or if it increases the conversions(bookings).

-   Converted is based on the data set given, there are two categories defined by logical value. It\'s going to show true when the customer completes bookings and it\'s going to show false when the customer visits the sites but not makes a booking.

### **Test Hypothesis**

-   **Null Hypothesis:** Both versions A and B have an equal probability of conversion or driving customer booking. In other words, there is no difference or no effect between A and B versions

-   **Alternative Hypothesis:** Versions both A and B possess different probability of conversion or driving customer booking and there is a difference between A and B version. Version B is better than version A in driving customer bookings. **PExp_B! = Pcont_A.**

### **Analysis in R**

**1. Prepare the dataset and load the tidyverse library which contains the relevant packages used for the analysis.**

```{r warning=FALSE, message=FALSE}
#import libraries
library(tidyverse)
```

```{r}
df <-read_csv("C:/Users/langa/OneDrive/Desktop/Dataset/AB_Website Results.csv")
head(df)
```

#### Let\'s filter conversions for variants A & B and compute their corresponding conversion rates

```{r}
(rate <- df %>%  group_by(variant) %>% 
                summarise(
                  observation=n(),
                  conversion=sum(converted=="TRUE"),
                  rate_coversion=conversion/n()
                          )
)
```

```{r}
#total variant convrsion
(a <- df %>%  select(variant,converted) %>% filter(variant=="A" ,converted=="TRUE") %>% 
  nrow()
)
```

```{r}
#conversion rate of A
(rate_a <- a/nrow(df %>% filter(variant=="A")))
```

```{r}
#treatment group -B
(b <- df %>%  filter(variant=='B' & converted=='TRUE') %>% nrow())
```

```{r}
#CONVERSION RATE OF B-TREATMENT GROUP
(rate_b <- b/nrow(df %>% filter(variant=='B')))
```

#### Let\'s compute the relative uplift using conversion rates A & B. The uplift is a percentage of the increase

```{r}
(uplift <- (rate_b-rate_a)/(rate_a)*100 
    )  %>% round(0)
```

This implies that **B** is better than **A** by **83%.** This is high enough to decide a winner

#### **Let\'s compute the pooled probability, standard error, the margin of error, and difference in proportion (point estimate) for variants A & B**

```{r}
# Pooled sample proportion for variants A & B 
(pool <- (rate_a +rate_b)/(a +b)
    )

```

```{r}
# Let's compute Standard error for variants A & B (SE_pool) 
(SE_pool <- sqrt(
  pool*(1-pool)*((1/a) +(1/b))
))
```

```{r}
# Let's compute the margin of error for the pool 
(ME <- SE_pool*qnorm(0.975))

```

```{r}
# Point Estimate or Difference in proportion
(dhat <- rate_b-rate_a)
```

#### Let\'s compute the z-score

```{r}
(z_score <- dhat/SE_pool)
```

#### Using this z-score, we can quickly determine the p-value via a look-up table, or using the code below:

```{r}
p_value <- pnorm(q = -z_score,  
                 mean = 0,  
                 sd = 1) * 2 
print(p_value) # 0.02571817
```

### **Recommendation & Conclusions**

-   Variant A has 20 conversions and 721 hits whereas Variant B has 37 conversions and 730 hits.

-   Relative uplift of 82.72% based on a variant A conversion rate is 2.77% and for B is 5.07%. Hence, variant B is better than A by 82.72%.

-   For this analysis P-value computed was **0.02571817**. Hence, there is strong statistical significance in test results.

-   From the above results that depict strong statistical significance. You should reject the null hypothesis and proceed with the launch.

-   Therefore, Accept Variant B and you can roll it to the users for 100%.

#### **Limitations**

It is one of the tools for conversion optimization and it\'s not an independent solution and it\'s not going to fix all the conversion issues of ours and it can\'t fix the issues as you get with messy data and you need to perform more than just an A/B test to improve on conversions. 

   
