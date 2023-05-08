Download Link: https://assignmentchef.com/product/solved-sta442-homework-1-generalized-linear-models
<br>
<h1>1          Flies</h1>

This is Ex. 6.81 from Faraway (2005). One hundred twenty-five fruit flies were divided randomly into five groups of 25 each. The response was the lifetime of the fruit fly in days. One group was kept solitary, while another was kept individually with a virgin female each day. Another group was given eight virgin females per day. As an additional control the fourth and fifth groups were kept with one or eight pregnant females per day (pregnant fruit flies will not mate). The thorax length of each male was measured as this was known to affect lifetime. The data is fruit fly in the library faraway. A complete reference to the data is given in

<table width="342">

 <tbody>

  <tr>

   <td width="258">the help file for the dataset.<strong>data</strong>(‘fruitfly’, package=’faraway’) <strong>summary</strong>(fruitfly)</td>

   <td width="84"> </td>

  </tr>

  <tr>

   <td width="258">##     thorax       longevity</td>

   <td width="84">activity</td>

  </tr>

  <tr>

   <td width="258">## Min.  :0.6400  Min.  :16.00</td>

   <td width="84">isolated:25</td>

  </tr>

  <tr>

   <td width="258">## 1st Qu.:0.7600 1st Qu.:46.00</td>

   <td width="84">one     :25</td>

  </tr>

  <tr>

   <td width="258">## Median :0.8400 Median :58.00</td>

   <td width="84">low     :25</td>

  </tr>

  <tr>

   <td width="258">## Mean  :0.8224  Mean  :57.62</td>

   <td width="84">many    :24</td>

  </tr>

  <tr>

   <td width="258">## 3rd Qu.:0.8800 3rd Qu.:70.00## Max.  :0.9400  Max.  :97.00</td>

   <td width="84">high    :25</td>

  </tr>

 </tbody>

</table>

Use a Gamma generalized linear model to model the lifetimes as a function of the thorax length and activity. Write a brief report (a half to one page of writing) summarizing the problem and the model used, and interpreting the coefficients in your model in terms of their effect on expected lifetime. Write a one-paragraph, non-technical, summary of the results, that might appear in a “Research News” media article about the laboratory in question.

<h2>Hints</h2>

<ul>

 <li>consider centering and rescaling variables</li>

 <li>don’t show R code in your answer but putting your code in an appendix might help the marker</li>

 <li>format tables and figures nicely</li>

 <li>The code below does not fit a useful model, but it might help you get started glm(thorax ~ longevity + activity, family=Gamma(), data=fruitfly)</li>

</ul>

<h1>2          Smoking</h1>

Over the course of the next 13 weeks you will be using the 2014 American <a href="http://www.cdc.gov/tobacco/data_statistics/surveys/nyts/index.htm">National Youth Tobacco Survey </a>to become an expert in all matters pertaining to the use of cigars, hookahs, and chewing tobacco amongst American school children. MS Access and SAS versions of the survey data are available from the Survey’s web page. On the <a href="http://pbrown.ca/teaching/appliedstats/data">pbrown.ca/appliedstats/astwo/data</a> page there is an R version of the 2014 dataset smoke.RData, a pdf documentation file 2014-Codebook.pdf, and the code used to create the R version of the data smokingData.R.

The research hypotheses to be investigated using this survey are as follows.

<ol>

 <li>Regular use of chewing tobacco, snuff or dip is no more common amongst Americans of European ancestry than for Hispanic-Americans and African-Americans, once one accounts for the fact that white Americans more likely to live in rural areas and chewing tobacco is a rural phenomenon.</li>

 <li>The likelihood of having used a hookah or waterpipe on at least one occasion is the same for two individuals of the different sexes, provided their age, ethnicity, and other demographic characteristics are similar.</li>

</ol>

Write a short consulting report addressing these hypotheses. This should include the following:

<ul>

 <li>a one-paragraph summary stating your conclusions, which could be understood by a child health and welfare professional or an executive in the marketing department of a large tobacco firm;</li>

 <li>a writeup of roughly one page of text (not including figures and tables) containing

  <ul>

   <li>an introduction restating the problem as you’ve interpreted it in relation to this dataset,</li>

   <li>a methods section giving the statistical models used (in mathematical notation, not R syntax) and justifying their use, and</li>

   <li>a results section where the results are described and interpreted; and</li>

  </ul></li>

 <li>an appendix containing your code.</li>

</ul>

The report will be assessed in terms of:

<ul>

 <li>clarity of presentation,</li>

 <li>the use of an appropriate model and implementing it correctly, • demonstration of an understanding of the statistical models used, and</li>

 <li>drawing conclusions which are consistent with the analysis.</li>

</ul>

<h2>The data</h2>

You can obtain the data with:

dataDir = “../data”

smokeFile = <strong>file.path</strong>(dataDir, “smokeDownload.RData”) <strong>if </strong>(!<strong>file.exists</strong>(smokeFile)) { <strong>download.file</strong>(“http://pbrown.ca/teaching/appliedstats/data/smoke.RData”, smokeFile)

}

(<strong>load</strong>(smokeFile))

## [1] “smoke”    “smokeFormats”

The smoke object is a data.frame containing the data, the smokeFormats gives some explanation of the variables. The colName and label columns of smokeFormats contain variable names in smoke and descriptions respectively.

<ul>

 <li>chewing_tobacco_snuff_or: RECODE: Used chewing tobacco, snuff, or dip on 1 or more days in the past 30 days</li>

 <li>ever_tobacco_hookah_or_wa: RECODE: Ever smoked tobacco out of a hookah or waterpipe The data produced by R has changed the data in a few ways.</li>

 <li>RuralUrban is a flag denoting whether the school the respondent attended was rural or urban.</li>

 <li>Race is an R factor recoded from RaceEth_no_mult_grp.</li>

 <li>ages have been converted to years from the original categorical variables described in the pdf file</li>

</ul>

<h2>Some words of advice</h2>

<ul>

 <li>Write in sentences and paragraphs.</li>

 <li>Provide captions for ALL figures and tables</li>

 <li>Don’t use default axis labels on plots and ensure text on plots is large enough to read comfortably</li>

 <li>Round numbers to 2 or 3 decimal places so tables look tidy.</li>

 <li>Don’t show raw R output. Put things in Latex or Markdown tables (using knitr::kable or Hmisc::latex)</li>

 <li>Give parameter estimates and confidence intervals on the ‘natural’ scale where possible (probabilities or odds rather than log-odds ratios)</li>

</ul>

<h2>Hints</h2>

get rid of 9 year olds because their data is suspicious smokeSub = smoke[smoke$Age &gt;= 10, ] fit a model incapable of answering the research question <strong>glm</strong>(ever_tobacco_pipe_not_hoo ~ RuralUrban + Race + Age,

family=binomial, data=smokeSub)

##

## Call: glm(formula = ever_tobacco_pipe_not_hoo ~ RuralUrban + Race


##  Age, family = binomial, data = smokeSub)

##

## Coefficients:

<table width="481">

 <tbody>

  <tr>

   <td width="49">##</td>

   <td width="237">(Intercept) RuralUrbanRural</td>

   <td width="112">Raceblack</td>

   <td width="84">Racehispanic</td>

  </tr>

  <tr>

   <td width="49">##</td>

   <td width="237">      -8.72748        0.20722</td>

   <td width="112">-1.23664</td>

   <td width="84">-0.15502</td>

  </tr>

  <tr>

   <td width="49">##</td>

   <td width="237">   Raceasian     Racenative</td>

   <td width="112">Racepacific</td>

   <td width="84">Age</td>

  </tr>

  <tr>

   <td width="49">##</td>

   <td width="237">      -0.97685       -0.04943</td>

   <td width="112">-0.51884</td>

   <td width="84">0.35989</td>

  </tr>

 </tbody>

</table>

##

## Degrees of Freedom: 20027 Total (i.e. Null); 20020 Residual

## (1939 observations deleted due to missingness)

## Null Deviance:    5884

## Residual Deviance: 5468 AIC: 5484

Looks like white kids smoke pipes more than anyone else.

<h1>References</h1>

Faraway, J.J. (2005). <em>Extending the Linear Model with R: Generalized Linear, Mixed Effects and Nonparametric Regression Models</em>. Chapman &amp; Hall/CRC Texts in Statistical Science. CRC Press. url: <a href="http://www.tandfebooks.com/isbn/9780203492284">http: </a><a href="http://www.tandfebooks.com/isbn/9780203492284">//www.tandfebooks.com/isbn/9780203492284</a>.