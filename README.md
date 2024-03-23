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


   
