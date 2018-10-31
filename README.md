 # APMC_CASE_STUDY-Analytics-Challenge
 
The Project is the Case Study of APMC Mandi Data

The Problem Statement is " The Ministry of Agriculture would like to assess trends in APMC (mandi) price and quantity arrival data for different commodities in Maharashtra. "

### The Objectives
* Test and filter outliers
* Understand price fluctuations and their seasonality
* Compare prices with the minimum support price (raw and deseasonalised)
* Flag set of APMC’s and commodities with the highest price fluctuations in each relevant season and year

### Files and Directories
* [APMC_final.ipynb](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/APMC_final.ipynb) - Jupypter Notebook containing the complete python Code
     * for Running the Jupyter Notebook it can be directly visualised in the browser 
      or if trouble viewing the file then Anaconda can be installed for Windows/Mac/Linux
      Then opening ananconda prompt and tehn starting the jupyter notebook to run APMC.ipynb
      and then running the python code
      
* [APMC_final.html](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/APMC_final.html) - The html file can be directly run in the browser to visualize the Jupyter notebook results

* [Data](https://github.com/ashushaw04/APMC_Argo_Challenge/tree/master/Data)  
    
    * CMO_MSP_Mandi.csv - MSP prices dataset
    * Monthly_data_cmo.csv - Monthly Mandi Data
    * Cleaned_APMC_monthly.csv - Containing the Dataet with the outliers Removed
    * DeseasonalisedData.csv - Containing the Data with Seasonality Removed
    * FlaggedFluctuations.csv - Containing the Data with Fluctuations Flagged

* [Images](https://github.com/ashushaw04/APMC_Argo_Challenge/tree/master/Images) - Containing all   the plots generated
    
## Methodology For the Analysis

> Please Note
> (the Jupyter Notebook contains the complete intuiton and the steps involved with more details about the whole process)

## 1. Initial Data Preparation
## 2. Outlier Removal
## 3. Seasonality Detection 
## 4. Seasonality Removal and MSP Prices Comparison
## 5. Flagging the Fluctuations

### Initial Data Preparation
The preliminary data processing involved first merging the data on the commodity names, cleaned to account for differences in the way commodities have been spelt across data sources. This yields a common dataset with all relevant variables, including prices, dates, MSP, and crop season.
We have further found a list of common commodities present in both our datsets i.e the "CMO_MSP_Mandi.csv" - MSP prices dataset "Monthly_data_cmo.csv" monthly mandi data. 
Thus we now consider only those data points which present in the common commosities which has 19 unique commodities.

### Outier Removal
Outliers are treated using standard statistical procedure, wherein all values not within the 25th to 75th percentile in the interquantile ranges are removed.
 In the Images Shown Below we can clealry see a set of outliers
 
![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Outlier%20Images/OutliersSORGUMJAWAR.png) ![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Outlier%20Images/OutliersPIGEON%20PEA%20TUR.png)



For Removing the ouliers we used the IQR Method thus obtained the CleanedDataset in Cleaned_APMC_monthly.csv
For removing the outliers we need to keep in mind that each commodity needs to be handled seperately for the removal of outliers ,thus we have handled each of the commodity seperately for outlier removal.



![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Outlier%20Images%20Removed/OutliersRemovedSORGUMJAWAR.png)![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Outlier%20Images%20Removed/OutliersRemovedPIGEON%20PEA%20TUR.png)

Thus we have clearly removed the outliers , the cleaned dataset which contains all the common commodities is stored in Cleaned_APMC_monthly.csv .

### Seasonality Detection

We consider only those APMC/commodity combinations with enough data to constitute a time series from which we can identify seasonality trends.

Let us take a look at the fluctuation in Bajri prices for the Mandi Jalgaon


![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/BajrijalgaonPrices.png)

We can clearly see the Fluctuations for the cluster Bajri and Jalgaon Mandi

Thus now we use the ACF and PACF Plots to check the stationarity of our data
and Finally the Dicky Fuller test is run to check the stationarity of the data

We can also see similar trends for different clusters of APMC and Commodity.
Some of them are shown below.


### Seasonality Removal and MSP Prices Comparison
First we checked the stationarity of the data using steps mentioned above.
Now we ise the statsmodel function seasonal_decompose() to see the Trend and
Seasonality in the timeseries data.
After ploting the curve obtained from the decompose function we clearly were able to
get a strong Trend Line and a period of repeating data a Seasonality pattern 
in out dataset.

Now to get the deseasonalised data we create out decompose function thus
the function **decompose ()** in the code is used to get the deseasonalised 
prices.

We have also implemented a checkModel() function to compare the residual erros obtained
from our decompose () finftion to calculate the acf and then decide uopn additive or miltiplicative 
model for decomposition the model with lower residuals is thus selected.

* Further  the two functions which can be clearly seen in the Jupyter Notebook
    * deseasonalise_data_mod( ) - Adds the deseasonalised prices to teh existing dataset
    * compareMSP( ) - Compares the MSP Prices , Modal Prices Raw and Deseasonalised
    These two functions need to be passed with the APMC and Commodity Cluster 
    
    Now we can see the results on few examples below
    
  
    ![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Price%20Comparison%20Raw%20and%20DeseasonalisedSample3.jpg) ![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Price%20Comparison%20Raw%20and%20DeseasonalisedSample2.jpg)  ![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Price%20Comparison%20Raw%20and%20DeseasonalisedSample1.jpg)  ![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Price%20Comparison%20Raw%20and%20DeseasonalisedSample4.jpg)    
    
    
    
### Flagging the Fluctuations
 
We first summarise the raw data, by grouping it by commodity, APMC and year, in that order. With this grouping, we can then calculate the greatest and least price observed in each year using the max_price and min_price information. This difference is calculated which is the fluctuation

Then the maximum fluctuations have been flagged and stored in FlaggedFluctuations.csv

## End Note
  * For better Understanding of the complete code please refer the Jupyter Notebook
  * We have used IQR method for outlier removal for simplfying the process and this process being the most intuitive one
  * For removing the Seasonality from data and deseasonalising the dataset we need to simple use the functions deserealise_data_mod()
   pass the relevant cluster of APMC and Commodity
  * Similarly for price comparison the compareMSP( ) needs to be used
    
    
