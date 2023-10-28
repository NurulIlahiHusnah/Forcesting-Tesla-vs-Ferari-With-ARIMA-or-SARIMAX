
# Share Price TESLA and FERARY

## Objective

"Ferrari and Tesla are two entities operating in the automotive industry. Ferrari, an established company with a longer history compared to the relatively newer entrant, Tesla, both showcase distinct innovations, capturing the admiration of numerous enthusiasts worldwide. However, to determine the superiority between them, an analysis of the comparative performance of their stocks from 2015 to 2023 will be conducted, demonstrating the extent of their competition in the market."

![tesla-y-ferrari](https://github.com/NurulIlahiHusnah/Forcesting-Tesla-vs-Ferari-With-ARIMA-or-SARIMAX/assets/125198828/f19be9af-8bd6-44f8-b3e3-02b701e7bf86)


## Data and Assumptions
The data used is
- Data TESLA and FERARI from 2015-2023.
- The dataset owned is a Time Series Forecasting dataset.
- The dataset contains 1885 rows and 7 columns
- Comprises comprehensive details of stock market trading data.

## Data Analysis
The data analysis process flow consists of:
### EDA (Exploratory Data Analysis)
Insights obtained from EDA results
    
    1. Comparison of the two stocks based on their peak prices.
 
![2](https://github.com/NurulIlahiHusnah/Forcesting-Tesla-vs-Ferari-With-ARIMA-or-SARIMAX/assets/125198828/6470da56-10fc-413a-b133-a0257f946673)


    2. Comparison of the two stocks based on their Volume.
![3](https://github.com/NurulIlahiHusnah/Forcesting-Tesla-vs-Ferari-With-ARIMA-or-SARIMAX/assets/125198828/897984fa-0ee3-4b3b-815a-deedc0da6983)


    3. Stock Price Race


https://github.com/NurulIlahiHusnah/Forcesting-Tesla-vs-Ferari-With-ARIMA-or-SARIMAX/assets/125198828/597ee578-ff8b-4960-80db-894dd15f910d



### Summary

"The surge in Tesla's stock price in 2020 was attributed to the company's remarkable innovation during that year, coinciding with the COVID-19 pandemic and the resulting economic recession that hindered oil production, impacting companies reliant on fossil fuels. This circumstance led to a decline in traditional automotive companies relying on gasoline. During that period, electric vehicles emerged as the favorable choice amid competition among competitors. However, Ferrari did not remain passive during the recession and pandemic. Despite being initially overshadowed by Tesla, Ferrari staged a resurgence, unveiling promising new innovations for its enthusiasts."


## Forecasting with SARIMAX

"Given the nature of the dataset focusing on stocks, it can be inferred that the time series characteristics are non-stationary. As the primary objective is to predict the trend movements of each stock, the 'Close' feature will be utilized as a key parameter for further analysis."














## Features

In data processing, several stages are carried out, namely: 
1. Check For Stationery

    Handle missing value and type data

        from statsmodels.tsa.stattools import adfuller
        def ad_test(dataset):
          dftest = adfuller(dataset, autolag= 'AIC')
          print("1. ADF : ",dftest[0])
          print("2. P-Value : ",dftest[1])
          print("3. Num Of Lags : ",dftest[2])
          print("4. Num Of Observations Used For ADF Regrssion and Critical Values Calculation : ", dftest[3])
          print("5. Critical Values :")
          for key, val in dftest[4].items():
            print("\t",key, " : ",val)

            
       ad_test(tesla['Adj Close'])
Output
        
        1. ADF :  -0.6172349754261902
        2. P-Value :  0.8670398792704236
        3. Num Of Lags :  0
        4. Num Of Observations Used For ADF Regrssion and Critical Values Calculation :  1884
        5. Critical Values :
	         1%  :  -3.433825707083533
	         5%  :  -2.8630753283581076
	         10%  :  -2.567587351898432


    ad_test(ferari['Close'])

Output

    1. ADF :  -0.48920474064411995
    2. P-Value :  0.8941059587398253
    3. Num Of Lags :  24
    4. Num Of Observations Used For ADF Regrssion and Critical Values Calculation :  1860
    5. Critical Values :
	     1%  :  -3.433870617038361
	    5%  :  -2.863095154794451
	    10%  :  -2.567597908717771

2. Differencing


![4](https://github.com/NurulIlahiHusnah/Forcesting-Tesla-vs-Ferari-With-ARIMA-or-SARIMAX/assets/125198828/dbc016e5-4a16-47ef-bcfe-ef500871d52c)

3. Determining optimal p, q with the Auto Arima model **(TESLA)**

        Best model:  ARIMA(3,0,1)(0,0,0)[0] intercept
        Total fit time: 19.281 seconds
                   SARIMAX Results
        Dep. Variable:	y	        No. Observations:	1861
        Model:	SARIMAX(3, 0, 1)	Log Likelihood	2924.292
        Date:	Sun, 15 Oct 2023	AIC	-5836.584
        Time:	02:20:48	        BIC	-5803.411
        Sample:	0	            HQIC	-5824.359  - 1861	

        Covariance Type:	opg		
        coef	std err	z	P>|z|	  [0.025	0.975]
        intercept	0.0003	0.000	1.618	0.106	-5.31e-05	0.001
        ar.L1	1.8227	0.034	52.988	0.000	1.755	1.890
        ar.L2	-0.7537	0.052	-14.520	0.000	-0.855	-0.652
        ar.L3	-0.0768	0.021	-3.659	0.000	-0.118	-0.036
        ma.L1	-0.8735	0.029	-29.964	0.000	-0.931	-0.816
        sigma2	0.0025	5.29e-05	47.653	0.000	0.002	0.003
        Ljung-Box (L1)     (Q):0.01	  Jarque-Bera (JB):	771.91
        Prob(Q):	0.91	              Prob(JB):	0.00
        Heteroskedasticity (H):2.10      Skew:	0.01
        Prob(H) (two-sided):	0.00	Kurtosis:	6.15


**Ferrari**

       ad_test(ferari['Adj Close'])

        1. ADF :  -0.48920474064411995
        2. P-Value :  0.8941059587398253
        3. Num Of Lags :  24
        4. Num Of Observations Used For ADF Regrssion and Critical Values Calculation :  1860
        5. Critical Values :
	        1%  :  -3.433870617038361
	        5%  :  -2.863095154794451
	        10%  :  -2.567597908717771


## Deployment

In this case I used the SARIMAX algorithm to do the modeling

### Ferarri  
                              SARIMAX Results                                
    ==============================================================================
    Dep. Variable:                  Close   No. Observations:                 1861
    Model:               SARIMAX(2, 0, 4)   Log Likelihood               10609.568
    Date:                Sat, 28 Oct 2023   AIC                         -21195.136
    Time:                        03:43:45   BIC                         -21128.790
    Sample:                             0   HQIC                        -21170.686
                               - 1861                                         
    Covariance Type:                  opg                                         
    ==============================================================================
                 coef    std err          z      P>|z|      [0.025      0.975]
------------------------------------------------------------------------------
    Open          -0.0058      0.001     -4.033      0.000      -0.009      -0.003
    High           0.0099      0.002      4.930      0.000       0.006       0.014
    Low            0.0058      0.003      2.264      0.024       0.001       0.011
    Volume     -9.036e-06   3.35e-05     -0.269      0.788   -7.48e-05    5.67e-05
    Adj Close      0.9897      0.002    462.574      0.000       0.986       0.994
    ar.L1          0.0268      0.004      6.559      0.000       0.019       0.035
    ar.L2          0.8835      0.004    211.429      0.000       0.875       0.892
    ma.L1          0.4866      0.005    105.823      0.000       0.478       0.496
    ma.L2         -0.3490      0.013    -25.857      0.000      -0.375      -0.323
    ma.L3          0.0307      0.021      1.482      0.138      -0.010       0.071
    ma.L4         -0.0223      0.026     -0.867      0.386      -0.073       0.028
    sigma2      6.459e-07   6.24e-09    103.448      0.000    6.34e-07    6.58e-07
    ===================================================================================
    Ljung-Box (L1) (Q):                 360.60   Jarque-Bera (JB):            789249.87
    Prob(Q):                              0.00   Prob(JB):                         0.00
    Heteroskedasticity (H):               0.25   Skew:                            -1.02
    Prob(H) (two-sided):                  0.00   Kurtosis:                       103.87
    ===================================================================================


![Ferarri](https://github.com/NurulIlahiHusnah/Forcesting-Tesla-vs-Ferari-With-ARIMA-or-SARIMAX/assets/125198828/e2e08f55-3b17-4ea3-b006-a4554711e4d6)



![5](https://github.com/NurulIlahiHusnah/Forcesting-Tesla-vs-Ferari-With-ARIMA-or-SARIMAX/assets/125198828/7ca11ff7-b6c9-4b96-b076-e793ef2729ec)


## Bussines Recommendation

"Conducting comprehensive market analyses consistently aids in informed decision-making and facilitates the identification of innovative strategies to be considered for future endeavors."
## 🔗 Links
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/)



## 🛠 Skills
PostgreSQL, Python, Tableau, Git, R, C++ , Oracle, Dbeaver, and Microsoft Office.


