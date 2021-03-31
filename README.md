# Real Estate Investing in Philadelphia

### Project Overview

For this project we are assuming the role of real estate investors in Philadelphia and our goal is to find the 5 best zipcodes to invest in. Specifically, we will be looking for the zipcodes with the highest return on investment (ROI), while attempting to mitigate risk. The investment period will be short term (1-3 years) as we are interested in keeping assets as fluid as possible. The data for this project comes from zillow.com and is comprised of the median home price in each zipcode in the US from April 1996 until April 2018. This file will serve as a high-level overview of the project, but I encourage you to check out the in-depth project in the Predicting_Real_Estate_Prices.ipynb file for the dataset and code.

### Selecting/Cleaning the Data

To begin, we trim this data down to all of the zipcodes in Philadelphia, PA. This leaves us with 35 zipcodes to model. While plotting all 35 zipcodes is a bit busy, a general shape of the data can be seen with the mean and median values.

![images/average_prices.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/average_prices.png)

The real estate boom and collapse is evidenced quite highly from 2004-2011 and would have a large impact on our model. I decided to begin my data at 2012 to provide a more stable data set to work with.

### ARIMA Modeling

After cleaning the data I began modeling on one zipcode. Here is the original time series plotted with rolling mean and std.

![images/zc_19111.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19111.png)

The time series is clearly not stationary, so I decided to difference it. Below is the differenced time series and its ACF and PACF.

![images/zc_19111_diff.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19111_diff.png)

![images/zc_19111_ACF.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19111_ACF.png)

From these graphs, I determined the order for our ARIMA model to be (0, 2, 0), so I ran our model and achieved these results:

![images/19111_model_results.jpg](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/19111_model_results.jpg)

![images/zc_19111_results.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19111_results.png)

The residuals don't look normally distributed, but this is the best I was able to get. My test predictions were pretty good though, achieving a RMSE of $3700. Here is an image of the test data.

![images/zc_19111_test.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19111_test.png)

Finally I used our model to predict prices for 3 years and calculated a return on investment for 1, 2, and 3 year periods. The return values (4%, 8%, and 12%) were not very promising and the risk estimates were large. I do not advise investing in this zipcode under the current model.

![images/zc_19111_forecast.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19111_forecast.png)

To continue on, I used some functions to quickly model the remaining 34 zipcodes and converted the results into a dataframe. I then used this dataframe to find the 5 zipcodes that have the highest ROIs. The zipcodes 19142, 19131, 19124, 19119, and 19136 produced the best predicted ROIs in all three time periods. I then remodeled these zipcodes to take a closer look and see if I could tune the parameters. The resulting test predictions and forecasts are displayed below.

Zipcode 19142:

![images/zc_19142_test.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19142_test.png)

![images/zc_19142_forecast.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19142_forecast.png)

Zipcode 19131:

![images/zc_19131_test.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19131_test.png)

![images/zc_19131_forecast.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19131_forecast.png)

Zipcode 19124

![images/zc_19124_test.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19124_test.png)

![images/zc_19124_forecast.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19124_forecast.png)

Zipcode 19119

![images/zc_19119_test.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19119_test.png)

![images/zc_19119_forecast.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19119_forecast.png)

Zipcode 19136

![images/zc_19136_test.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19136_test.png)

![images/zc_19136_forecast.png](https://github.com/CGrannan/dsc-mod-4-project-online-ds-sp-000/blob/master/images/zc_19136_forecast.png)

### Anaysing Results

To account for risk in my investments, I look at the size of my investment (price of home in each zipcode compared to the median home prices in Phily), the RMSE from the test models (representing the risk of using my model), and the shape of my confidence intervals (representing the volatility of that zipcode). From assessing these details, I concluded that zipcodes 19142, 19124, 19119, and 19136 are worth investing in because the predicted gains outweigh the risks. I would not invest in zipcode 19131 based off of this model as the testing accuracy is not strong enough to have faith in the predictions.

### Future Work

Moving forward, I would bring in other features to the dataset to see if we can refine the fit on our models. Using financial (tax rates, income levels) or social (school districts, crime rates) information would allow further tuning of our model. I would also consider using some different types of models like SARIMA to see if we can get tighter results for some of our potentially high ROI zipcodes. For now though, we have identified some good opportunities for investment!

### Files

Data contains the zillow data that is used in the notebook.

Images is a folder containing several graphs from the notebook.

Predicting_Real_Estate_Prices.ipynb is the notebook that contains our code and analysis.