# Trading

A simple script to perform technical analysis on stocks using the EMA, MACD, OBV, RSI, and Bollinger Band indicators. This script can plot these indicators and find buy/sell signals.

## Install

The following modules need to be installed using the following commands:

```
pip install matplotlib 
pip install TA-Lib
pip install numpy
pip install yahooquery
pip install yahoo-fin
```

## Usage

See demo.py for the code needed to perform technical analysis and documentation for full documentation on the functions available.

First an object is created for the stock, this example uses Amazon (ticker - amzn) as an example.

```python
import stock_functions as sf

stock = sf.Equity("amzn")
````

Actions can be performed for the stock using the stock object. First we need to get historical data for the stock.

```python
stock_history = stock.get_history()
```

Now we can perform simple technical analyis on the stock.

```python
stock_ma_signal = stock.get_ma_signal(show_plot=1)
stock_macd_signal = stock.get_macd_signal(show_plot=1)
stock_obv_signal = stock.get_obv_signal(show_plot=1)
stock_rsi_signal = stock.get_rsi_signal(show_plot=1)
stock_bb_signal = stock.get_bollinger_band_signal(show_plot=1)
```

The output is shown below:
![EMA picture](https://github.com/RemiBahar/Trading/blob/master/images/EMA.png)
![MACD picture](https://github.com/RemiBahar/Trading/blob/master/images/MACD.png)
![OBV picture](https://github.com/RemiBahar/Trading/blob/master/images/OBV.png)
![RSI picture](https://github.com/RemiBahar/Trading/blob/master/images/RSI.png)
![BB picture](https://github.com/RemiBahar/Trading/blob/master/images/BB.png)

## Documentation

### get_history

Parameters:

**start_date** : str in the form yyyy-mm-dd, default: 365 days ago

First date to get stock data for

**end_date** : str in the form yyyy-mm-dd, default: today's date

Last date to get stock data for

**period** : str, default: 1d

Period to get the data. 1d, 1m, etc

**show_plot** : int 0 or 1, default: 0

Decides whether to plot a graph of the stock's price. Will output a graph if 1 and will not output a graph if 0

Returns: 

**ticker_df**: 

A dataframe containing the low, open, close, high, adjclose price of the stock and volume for each day 

### get_ma_signal

Parameters:

**ema_short_period**: int, default:10

The period (in days) for which to calculate the short EMA.

**ema_long_period**: int, default: 50

The period (in days) for which to calculate the long EMA.

**show_plot**: int 0 or 1, default: 0

Decides whether to plot a graph of the stock's price and EMA. Will output a graph if 1 and will not output a graph if 0.
By default 50-day EMA, 10-day EM

Returns:

**return_dict**: dict of results. The keys are listed below

* **ma_signal**: str, current EMA signal which can be bullish or bearish

* **ma_crossover**: datetime, datetime of last EMA crossover event

* **ma_trend**: str, relationship between long and short EMA which can be converging or diverging

* **ma_seperation**: float, difference in price between long and short EMA
  
### get_macd_signal

Parameters:

**show_plot**: int 0 or 1, default: 0

Decides whether to plot a graph of the stock's signal and MACD. Will output a graph if 1 and will not output a graph if 0.

Returns:

**return_dict**: dict of results. The keys are listed below

* **last_crossover**: str, current MACD signal which can be bullish or bearish

* **last_crossover_date**: datetime, datetime of last MACD crossover event

* **latest_diff_percentage**: float, percentage difference between MACD and signal

### get_obv_signal

Parameters:

**show_plot**: int 0 or 1, default: 0

Decides whether to plot a graph of the stock's OBV. Will output a graph if 1 and will not output a graph if 0.

Returns:

**return_dict**: dict of results. The keys are listed below

* **obv_type**: str, current OBV signal which can be bullish, bearish or neutral depending on if the OBV has broken above a range, below    a range or is still in the range

* **diff_percentage**: float, percentage OBV is above the upper line if OBV is bullish or the percentage OBV is below the lower line if   OBV is bearish

* **obv_gradient_type**: str, increasing, decreasing or flat depending on if the latest OBV has increased, decreased or remained the       same since the previous OBV

* **date_diff**: int, days since OBV broke out of range

### get_rsi_signal

Parameters:

**show_plot**: int 0 or 1, default: 0

Decides whether to plot a graph of the stock's RSI. Will output a graph if 1 and will not output a graph if 0.

Returns:

**return_dict**: dict of results. The keys are listed below

* **rsi_data**: array of rsi values

* **rsi_signal**: str, overbought, oversold or neutral depending on if RSI is above 70, below 30 or between 70 and 30

* **rsi_value**: float, current rsi value

* **rsi_crossover**: datetime, datetime of last rsi crossover (if RSI is overbought or oversold)

* **rsi_trend**: str, decreasing, increasing or flat depending on if the latest RSI has decreased, increased or remained the same since   the previous RSI
  
  ### get_bollinger_band_signal
  
Parameters:

**show_plot**: int 0 or 1, default: 0

Decides whether to plot a graph of the stock's Bollinger Bands and price. Will output a graph if 1 and will not output a graph if 0.

Returns:

**return_dict**: dict of results. The keys are listed below

* **bb_signal**: str, bulish, bearish or neutral depending on if the price has gone below the lower bollinger band, above the upper bollinger band or is between the bands.

* **bb_crossover**: datetime, datetime of last Bollinger crossover (if bb_signal is bullish or bearish)

* **bb_trend**: str, increasing, decreasing or flat depending on if the latest price has increased, decreased or remained the same since the previous closing price

* **bb_width_min**: float, lowest historic seperation between the lower and upper bollinger bands

* **bb_width_average** float, mean historic seperation between the lower and upper bollinger bands

* **bb_width**: float, current seperation between lower and upper bollinger bands
