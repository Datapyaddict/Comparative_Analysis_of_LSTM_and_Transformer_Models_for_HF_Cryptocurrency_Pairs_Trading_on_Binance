# A Comparative Analysis of LSTM and Transformer Models for High-Frequency Cryptocurrency Pairs Trading on the Binance Exchange   
### University of York (UK) /Msc in Computer Science with AI/ Research Project
***

## Table of Contents
[1. Abstract](#Abstract)  
[2. Research Project's Overview](#Research_Project_Overview)  
[3. Artefact Repository Tree Architecture](#Artefact_Repository_Tree_Architecture)  
[5. Jupyter Notebooks](#Jupyter_Notebooks)  


****

<a id = 'Abstract'></a>
## 1. Abstract

The aim of this research is twofold: 
> first, to compare the predictive capabilities of two vanilla __Deep Learning models (DL)__, __Long Short-Term Memory (LSTM)__ and __Transformer__, specifically focusing on __high-frequency__ (HF) __cryptocurrencies__ forming __cointegrated pairs__ over the period from 01/01/2023 to 23/01/2023. 

> Second, leveraging the optimal DL model, the study examines the profitability of different __AI-based algorithmic pair trading__ (PT) strategies against traditional __rule-based algorithmic PT__ strategies within a __back-testing__ framework, with an emphasis on identifying the conditions under which the AI-based strategies can outperform the traditional ones.

The motivation for this work arises primarily from the __high volatility__ observed in cryptocurrency markets compared to other financial markets, offering a unique opportunity to investigate the __statistical characteristics__ of HF cointegrated cryptocurrencies. Additionally, while LSTM models have demonstrated success in PT applications, there is limited literature on the integration of Transformers into algorithmic PT, highlighting the need for further exploration in this area.

From an ethical perspective, this research does not involve any human or qualitative data. However, integrating complex ML models into trading decisions raises accountability issues. These models can carry biases that may influence outcomes against certain cryptocurrencies. Additionally, when combined with algorithmic trading, ML models can enhance opportunities for market manipulation. For individuals without access to advanced ML-based algorithmic trading technology, this creates economic inequalities.

The methodology follows a systematic approach involving several steps. First, the __most liquid pairs__ are identified using the __monetary volume__. Then, cointegrated pairs are determined in the __in-sample period__ and evaluated in the __out-of-sample period__. Based on the actual prices of the coins forming the pairs over the respective in-samples and out-of-samples, two vanilla LSTM and Transformer models are trained and evaluated to ensure acceptable processing time. Vanilla Transformers were found to significantly outperform vanilla LSTM models in terms of processing time and errors and were used to predict prices, from which the predicted spreads were calculated and compared to the actual spreads. The pairs that exhibit low __prediction errors__ and __high correlation__ and __cointegration__ relationships in the predicted spreads are elected for PT. 
The predicted and actual spreads were then used in algorithmic PT strategies using the __rolling Z-score__ and different rolling windows, resulting in multiple PT strategies. 

The study found that the financial performance of Transformer-based PT significantly underperformed compared to rule-based algorithmic PT when evaluated using the __Sharpe ratio__, annualised return, and win ratio. This aligns with the fact that Transformer-based PT is significantly riskier, involving a higher number of trades, increased fees, shorter average duration, and a greater maximum drawdown. 



<a id = Research_Project_Overview></a>
## 2. Research Project's Overview

The __Master's dissertation__ of the project can be found [here](https://github.com/Datapyaddict/Comparative_Analysis_of_LSTM_and_Transformer_Models_for_HF_Cryptocurrency_Pairs_Trading_on_Binance/blob/main/DOCUMENTS/Msc_in_CS%20with_AI-Research_Project_Dissertation.pdf).
The experiment follows several steps as described in the below diagram.

<picture>
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/Datapyaddict/Comparative_Analysis_of_LSTM_and_Transformer_Models_for_HF_Cryptocurrency_Pairs_Trading_on_Binance/blob/main/PICTURES/experiment_diagram.png">
  <img src="https://github.com/Datapyaddict/Comparative_Analysis_of_LSTM_and_Transformer_Models_for_HF_Cryptocurrency_Pairs_Trading_on_Binance/blob/main/PICTURES/experiment_diagram.png" width="800">
</picture>

This project uses __Google Colab__ and the AT100 GPU facility to build DL models.
The artefacts consist of :
1. a database SQLite [binance_prices.db](https://www.kaggle.com/datasets/anhtuanng/binance-prices) (Size 2.3 Go) located on __Kaggle__. It contains __minute-interval cryptocurrency prices__ for all __USDT quoted coins__ in __Binance__, and  covers the period of January 2023.

2. __5 Jupyter notebooks__ that have to be run sequentially: 
    - `script_1.ipynb`,
    - `script_2.ipynb`,
    - `script_3.ipynb`,
    - `script_4.ipynb`,
    - `script_5.ipynb`.

3. __27 LSTM models and 27 Transformer models__ generated by the script `script_3.ipynb`.

4. various output files from the scripts.


<a id = 'Artefact_Repository_Tree_Architecture'></a>
## 3. Artefact Repository Tree Architecture

The following folders have to be created manually in Google Colab. 
It is worth noting that all sub folders are created by the __Jupyter notebooks__.

    - drive/MyDrive/PROJECT/binance_prices.db
    - drive/MyDrive/PROJECT/SPREADS/ACTUAL/*
    - drive/MyDrive/PROJECT/PRICES/ACTUAL/*
    - drive/MyDrive/PROJECT/PRICES/PREDICTED/*
    - drive/MyDrive/PROJECT/MOST_LIQUID_COINS/*
    - drive/MyDrive/PROJECT/MOST_COINTEGRATED_PAIRS/*
    - drive/MyDrive/PROJECT/MODELS/*
    - drive/MyDrive/PROJECT/EXPLORATIVE_DATA_ANALYSIS/*
    - drive/MyDrive/PROJECT/BACKTESTING/*
    - drive/MyDrive/Colab Notebooks/PROJECT/SCRIPTS/*

The database [binance_prices.db](https://www.kaggle.com/datasets/anhtuanng/binance-prices) must be placed at the root of the project folder in Google Colab, after it is built locally by running the notebook `script_1.ipynb`. Indeed, it is not possible to run the latter in Google Colab to fetch Binance prices.

The artefacts from the repository need to be placed according to their respective paths in the project folder.

The Jupyter Notebooks have to be placed in a dedicated folder named __"Colab Notebooks"__ in Google Colab for them to be able to run.
If necessary, do not hesitate to adjust the paths referenced in the scripts.

The path drive/MyDrive/PROJECT/MODELS/ contains 34 DL models.

The folders `SPREADS`, `PRICES`, `MOST_LIQUID_COINS`, `EXPLORATIVE_DATA_ANALYSIS`, `BACKTESTING` and `MOST_COINTEGRATED_PAIRS` contain output csv files generated by the scripts.





<a id = 'Jupyter_Notebooks'></a>
## 4. Jupyter Notebooks

The following Jupyter notebooks are found in ./SCRIPTS folder.

<table>
<tr>
    <th> Jupyter Notebook Name </th>
    <th> Inputs  </th>
    <th> Functions</th>
    <th> Runtime </th>
    <th> Outputs </th>
</tr>

<tr>
    <td rowspan = "2"> script_1</td>
    <td rowspan = "2">Binance API with minute-interval prices, 
    
 start and end dates of the period for which the market data are fetched.</td>
    <td>Get market data from Binance API.</td>
    <td rowspan = "2">1 hour</td>
    <td rowspan = "2">The database `binance_prices.db` at the root of the project folder.</td>
</tr>

<tr>
    <td>Save the data into an SQLite database</td>
</tr>

<tr>
    <td rowspan = "5"> script_2</td>
    <td rowspan = "5">Use the database `binance_prices.db` to get market prices.</td>
    <td>Produce the list of the most liquid coins in the in-sample period.</td>
    <td rowspan = "5">30 minutes</td>
    <td> File containing the most liquid coins for the in-sample. Results were used in Table.A7 in the dissertation.
        
Ex:

     ./MOST_LIQUID_COINS/top_25th_market_caps_from_2023-10-01_to_2023-11-30.csv
</td>
</tr>

<tr>
        <td>Produce the list of cointegrated pairs during this period.</td>
        <td>Temporary file containing all potential cointegrated pairs:
        
Ex:

    ./MOST_COINTEGRATED_PAIRS/cointegrated_pairs_2023-01-01_2023-06-30_2023-07-31.csv
</td>
</tr>    

<tr>
    <td>Extract the statistical properties of the cointegrated pairs during the in-sample and out-of-sample periods</td>
    <td>Refined list of cointegrated pairs used in Table.A8 in the dissertation :
    
    ./MOST_COINTEGRATED_PAIRS/confirmed_cointegrated_pairs.csv

</td>
</tr>   
    
<tr>
    <td>Output and plot the actual prices for the coins forming the cointegrated pairs in the training/test sets. They will be used to train/test the DL models.</td>
    <td>Files representing the train/test sets and containing the actual mid prices of coins forming the pairs and their plots. They are used to train/test the DL models.

Ex:

    ./PRICES/ACTUAL/MID_plot_DOGEUSDT_MATICUSDT.png
    ./PRICES/ACTUAL/training_set_MATICUSDT_2023-03-01_2023-08-31.csv
    ./PRICES/ACTUAL/test_set_MATICUSDT_2023-08-31_2023-09-30.csv
</td>
</tr>   

<tr>
    <td>Calculate and output the corresponding actual spreads.</td>
    <td>Files containing the actual spreads of the pairs and their plots. They are used to evaluate the predicted spreads.
    
Ex:

    ./SPREADS/ACTUAL/actual_spread_DOGEUSDT_MATICUSDT_2023-03-01_2023-09-30.csv
    ./SPREADS/ACTUAL/actual_spread_plot_DOGEUSDT_MATICUSDT.png
</td>
</tr>

<tr>
    <td rowspan = "2"> script_3</td>
    <td rowspan = "2">Use the train/test sets produced by script_2.</td>
    <td>Build the Transformer and LSTM models for each coin involved in a cointegrated pair. Save the models with h5 and pth extensions.</td>
    <td rowspan = "2">12 hours</td>
    <td>34 files containing the DL models.

Ex:

    ./MODELS/transformer_model_TRXUSDT_2023-06-01_2023-11-30.pth
    ./MODELS/lstm_model_XRPUSDT_2023-06-01_2023-11-30.h5
</td>
</tr>

<tr>
    <td>Predict and plot the prices of the coins forming the pairs over the out-of-sample periods.</td>
    <td>
    
- Csv files containing Price predictions. 
- Plots displaying the predicted vs actual prices over the out-of-sample. They are used for the plots Figure.6, Figure.7, Figure.9, Figure.10, Figure.12, Figure.13, Figure.15, Figure.16  in the dissertation.
- The models’ performance file (models_performance.csv) used in Table.A9 in the dissertation.

Ex:

    ./PRICES/PREDICTED/transformers_predictions_DOGEUSDT_2023-08-31_2023-09-30.csv    
    ./PRICES/PREDICTED/transformers_predictions_DOGEUSDT_2023-08-31_2023-09-30.png
    ./PRICES/PREDICTED/lstm_predictions_DOGEUSDT_2023-08-31_2023-08-31.png    
    ./PRICES/PREDICTED/lstm_predictions_DOGEUSDT_2023-08-31_2023-09-30.csv    
    ./PRICES/PREDICTED/models_performance.csv
</td>
</tr>

<tr>
    <td rowspan = "6"> script_4</td>
    <td rowspan = "6">Actual and predicted spreads.</td>
    <td>Generate pair-trading signals based on predicted spreads, open and close transactions.</td>
    <td rowspan = "6">3 hours</td>
    <td rowspan = "6">
    
Backtesting results are output in sub-folders per cointegrated pair:
- ai_algo_trading_data_* files contain the AI-APTS trading signals.
- standard_algo_trading_data_* files contain the RB-APTS trading signals.
- portfolio_ai_algo_* files contain the financial results for back-tested AI-APTS.
- portfolio_standard_algo_* files contain the financial results for back-tested RB-APTS.

Ex: 

    ./BACKTESTING/DOGEUSDT_MATICUSDT_2023-03-01_2023-08-31_2023-09-30/ai_algo_trading_data_DOGEUSDT_MATICUSDT_2023-08-31_2023-09-30_360min_window_3min_delay.csv
    
    ./BACKTESTING/DOGEUSDT_MATICUSDT_2023-03-01_2023-08-31_2023-09-30/standard_algo_trading_data_DOGEUSDT_MATICUSDT_2023-08-31_2023-09-30_360min_window_3d_delay.csv
    
    ./BACKTESTING/DOGEUSDT_MATICUSDT_2023-03-01_2023-08-31_2023-09-30/portfolio_ai_algo_DOGEUSDT_MATICUSDT_2023-08-31_2023-09-30_360_min_window_3d_delay.csv
    
    ./BACKTESTING/DOGEUSDT_MATICUSDT_2023-03-01_2023-08-31_2023-09-30/portfolio_standard_algo_DOGEUSDT_MATICUSDT_2023-08-31_2023-09-30_360_min_window_3d_delay.csv
    
    
Aggregated results from the back-testing :

    ./BACKTESTING/back_testing_results.csv
    

Outputs related to the actual and predicted spreads:
    
    ./SPREADS/PREDICTED/predicted_spreads-statistical_properties.csv used to produce the final list of pairs eligible for PT.

    ./SPREADS/PREDICTED/pred_vs_actual_error_metrics.csv used to produce the final list of pairs eligible for PT.

    ./SPREADS/ACTUAL/actual_spreads-statistical_properties.csv. 

Plots of the predicted and actual spreads. They are used to produce Figure.5, Figure.8, Figure.11, and Figure.14 in the dissertation.

Ex : 

    ./SPREADS/PREDICTED//PREDICTED_VS_ACTUAL_SPREAD_DOGEUSDT_MATICUSDT_2023-08-31_2023-09-30_plot.png


</td>
</tr>
<tr>
    <td>Generate pair-trading signals based on actual spreads, open and close transactions.</td>
</tr>
<tr>
    <td>calculate portfolio trading results from the 2 trading signals.</td>
</tr>
<tr>
    <td>calculate the predicted spreads.</td>
</tr>
<tr>
    <td>compare and plot the actual vs predicted spreads.</td>
</tr>
<tr>
    <td>calculate cointegration and correlation properties for the predicted spreads.</td>
</tr>



<tr>
    <td rowspan = "3"> script_5</td>
    <td rowspan = "3">
        Backtesting results, models' performance results.    
    </td>
    <td>Get statistical properties from the back-testing results.</td>
    <td rowspan = "3">5 min</td>
    <td rowspan = "3">
    
 Csv files from significance and statistical tests are output in the folder `EXPLORATIVE_DATA_ANALYSIS`:

-	all_stats.csv is used to produce Table.A10 in the dissertation.
-	all_stats_models.csv is used to produce Table.2 in the dissertation.
-	average_trade_duration_distribution_plot.png
-	fees_distribution_plot.png
-	net_pnl_distribution_plot.png
-	number_of_trades_distribution_plot.png
-	one_sample_result.csv is used to produce Table.6 in the dissertation.
-	one_sample_result_models.csv is used to produce Table.3 in the dissertation.
-	scope.csv is used to produce Table.4 in the dissertation.
-	sharpe_ratio_distribution_plot.png is used to produce Figure.17 in the dissertation.
-	two_samples_result.csv is used to produce Table.5 in the dissertation.
-	two_samples_result_models.csv is used to produce Table.1 in the dissertation.
</td>
</tr>
<tr>
    <td>Get the statistical properties of models’ performance.</td>
</tr>
<tr>
    <td>Apply significance tests to back-testing and models’ performance results.</td>
</tr>
  
</table>    
    







