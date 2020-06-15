# Trading

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


