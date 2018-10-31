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
    
## Methodology

> Please Note
> (the Jupyternotebook contains the complete intuiton and the steps involved with more details about the whole process)

## 1. Initial Data Preparation
## 2. Outlier Removal
## 3. Seasonality Detection 
## 4. Seasonality Removal and MSP Prices Comparison

### Initial Data Preparation
The preliminary data processing involved first merging the data on the commodity names, cleaned to account for differences in the way commodities have been spelt across data sources. This yields a common dataset with all relevant variables, including prices, dates, MSP, and crop season.

### Outier Removal
Outliers are treated using standard statistical procedure, wherein all values not within the 25th to 75th percentile in the interquantile ranges are removed.
 he Images Shown Below we can clealry see a set of outliers
 
![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Outlier%20Images/OutliersSORGUMJAWAR.png) ![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Outlier%20Images/OutliersPIGEON%20PEA%20TUR.png)



For Removing the ouliers we used the IQR Method thus obtained the CleanedDataset in Cleaned_APMC_monthly.csv
for removing the outliers we need to keep in mind that each comoodity needs to be handled seperately for the removal of outliers



![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Outlier%20Images%20Removed/OutliersRemovedSORGUMJAWAR.png)![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Outlier%20Images%20Removed/OutliersRemovedPIGEON%20PEA%20TUR.png)

Thus we have clearly removed the outliers

### Seasonality Detection

We consider only those APMC/commodity combinations with enough data to constitute a time series from which we can identify seasonality trends.

Let us take a look at the fluctuation in Bajri prices for the Mandi Jalgaon


![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/BajrijalgaonPrices.png)

We can clearly see the Fluctuations

Thus now we use the ACF and PACF Plots to check the stationarity of our data
and Finally the Dicky Fuller test is run to check the stationarity of the data

### Seasonality Removal and MSP Prices Comparison
* Two functions which can be clearly seen in the Jupyter Notebook
    * deseasonalise_data_mod( ) - Adds the deseasonalised prices to teh existing dataset
    * compareMSP( ) - Compares the MSP Prices , Modal Prices Raw and Deseasonalised
    These two functions need to be passed with the APMC and Commodity Cluster 
    
    Now we can see the results on few examples below
    
  
    ![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Price%20Comparison%20Raw%20and%20DeseasonalisedSample3.jpg) ![alt text](https://github.com/ashushaw04/APMC_Argo_Challenge/blob/master/Images/Price%20Comparison%20Raw%20and%20DeseasonalisedSample2.jpg)
    
    
### Flagging the Fluctuations
 
We first summarise the raw data, by grouping it by commodity, APMC and year, in that order. With this grouping, we can then calculate the greatest and least price observed in each year using the max_price and min_price information. This difference is calculated which is the fluctuation

Then the maximum fluctuations have been flagged and stored in FlaggedFluctuations.csv

## End Note
  * For better Understanding of the complete code please refer the Jupyter Notebook
  * We have used IQR method for outlier removal for simplfying the process and this process being the most intuitive one
  * For removing the Seasonality from data and deseasonalising the dataset we need to simple use the functions deserealise_data_mod()
   pass the relevant cluster of APMC and Commodity
  * Similarly for price comparison the compareMSP( ) needs to be used
    
    
