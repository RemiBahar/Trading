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

return_dict: dict of results. The keys are listed below

**ma_signal**: str, current EMA signal which can be bullish or bearish

**ma_crossover**: datetime, datetime of last EMA crossover event

**ma_trend**: str, relationship between long and short EMA which can be converging or diverging

**ma_seperation**: float, difference in price between long and short EMA

