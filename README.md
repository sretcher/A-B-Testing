Spencer Retcher
[sretcher.github.io](https://github.com/sretcher/sretcher.github.io)

### A/B Testing (Comparing Two Independent Population Proportions)

In Survey Methodology (Dec. 2013), factors that influence survey reponse rates were investigated. A designed experiment allowed Web users to interact with two different versions of surveys. One format used a welcome screen with a white background and the other used a welcome screen with a red background. The break-off-rates (the porportion of sampled users who quit the survey before completing it) was recorded for both formats. We will use a two sample test of hypothesis about (p1 - p2) to find if the true break-off-rate is lower for the format with the red welcome screen than the format with the white welcome screen. 

|       | White Welcome Screen          | Red Welcome Screen |
| ------------- |:-------------:| -----:|
| Number of Web users     | 190| 183 |
| Number who break off survey     | 49      |   37 |
| Break-off rate |.258 | .202


### Conditions Required for Vaid Large-Sample Inferences about (p1 - p2)
1. The two samples are randomly selected in an independent manner from the two populations.
2. The sample sizes, n1 and n2, are large.


We will consider the first assumption to be fulfilled since customers interacted with surveys that had a randomly selected format. To see if our sample sizes are large enough, we use the formulas (n1)(p1) >= 15 (n1)(q1) >= 15 and (n2)(p2) > 15 (n2)(q2) > 15. 

Since (190)(.258) = 49 (190)(.742) = 141 (183)(.202) = 37 (183)(.798) = 146, we will consider the second assumption to be fulfilled. Having a large sample size means that by the CLT, the sampling distribution of p1 - p2 will be normal, which is why we will use the standard normal z statistic as the test statistic. 

### Large Sample of Hypothesis about (p1 - p2)
Let p1 be the true break-off-rate for surveys with a red welcome screen and p2 be the true break-off-rate for surveys with a white welcome screen. We will conduct this test with a level of significance of 0.1.

Ho: p1 - p2 = 0

Ha: p1 - p2 < 0


### Analysis.
We can form our z statistic with the equation (p1 - p2 - 0 ) / sqrt ( p1q1/n1 + p2q2/n2). Under the null hypothesis, p1 = p2. That means by taking the weighted average of p1 and p2, we get a better estimate of p than p1 or p2 individually. (49 + 37)/(190 + 183) = .23 which is our pooled sample proportion. Substituting this value into our equation, we get (.202 - .258) / sqrt( (.23)(.77)(1/183 + 1/190) = -1.28. 

Looking at a table, we find that the z-value corresponding to an area of .01 is 2.3263. Since -1.28 > 2.3263, we do not reject the null hypothesis. We do not have enough evidence to prove that welcome screen color reduces break-off rates. The p-value for this test is P(z <-1.28) = .5 - .3997 = 0.1003.

We can construct a 99% confidence interval with the formula .202 - .258 + 2.3263 * sqrt( (.202)(.798)/183 + (.258)(.742)/190 ) = (-Inf, 0.045). We are 99% confident that the true break-off-rate of p1 is (-Inf, 0.045) lower/above the true break-off-rate of p2.


### Running the Test in R
When using ```prop.test```, make sure that x is a vector of successes for both proportions and n is a vector of corresponding sample sizes. 

```
prop.test(x = c(37,49),n=c(183,190),alternative = "less",conf.level = .99)

#	2-sample test for equality of proportions with
#	continuity correction
#
# data:  c(37, 49) out of c(183, 190)
# X-squared = 1.3318, df = 1, p-value = 0.1242
# alternative hypothesis: less
# 99 percent confidence interval:
# -1.0000000  0.0507573
# sample estimates:
#   prop 1    prop 2 
# 0.2021858 0.2578947 
```


