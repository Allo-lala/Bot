
### rr
`pip3 install -r requirements.txt`

KGF8DQ9!YPxK5w8


### Run other bots
`python3 po_bot_indicators.py`
to run trading bot with strategy based indicators (only Mac and Linux users)

`python3 po_bot_ml.py`
to run trading bot with Machine Learning for prediction (only Mac and Linux users)

### Other scripts
`python3 test_on_historical_data.py`
to test your strategies on historical data (only Mac and Linux users)

### After authorization:
- set timeframe as `1 min`
- set time as `1 min`

### Information
Bot connects to websocket and receives signals every half a second from PO.
To make it more convenient, I simplify data to 1 second so that to use seconds
everywhere. After each change of currency, the screen reloads. It is to cut
unwanted signals from previous currencies.

### Pocket Option trading bot Martingale
`po_bot.py` - Martingale trading. The default strategy is pretty simple. If the previous candles are red, the bot makes 'put' order. And 'call' otherwise. You can see a current Martingale stack in the console (Martingale stack). For example, Martingale stack [1, 3, 7, 15, 31, 62, 124, 249, 499, 999] means that if you order $1 and lose, the next order will be $3, then $7, and so on. You can change `MARTINGALE_COEFFICIENT`.

### Pocket Option trading bot with indicators
`po_bot_indicators.py` - script allows you to try different indicators and their combinations. See how an example in `check_indicators()` works and make your updates. Currently, the PSAR strategy is used. Despite using default parameters `acceleration_step=0.02`, `max_acceleration_factor=0.2`, bot's sensitivity is higher, so additional orders appear. Works for 1m and higher timeframes. 
Only for Mac, Linux, .NET6.0 or newer required: https://dotnet.microsoft.com/en-us/download/dotnet/6.0

### Pocket Option trading bot with machine learning
`po_bot_ml.py` - script makes orders based on prediction. Random Forest Classifier approach is used. The prediction is based on the indicators: `awesome_oscillator`, `PSAR`, `CCI` and `MACD` from the last 200 candles. Bot makes an order when the probability is > 0.60. You can set even higher values (0.70, 0.80, 0.90) in the `check_data()` method. !important! You have to set an order time = TIME param. For example, your `po_bot_ml.py/TIME`=5, then set your order time to 5 minutes. The bot make a prediction only for PUT action. And if probability < 30%, then CALL action fires. Works for 1m and higher timeframes. Works for 1m and higher timeframes. 
Only for Mac, Linux, .NET6.0 or newer required: https://dotnet.microsoft.com/en-us/download/dotnet/6.0

### Backtest
`test_on_historical_data.py` - here you can backtest strategies on historical data of 1m and 5m timeframes. To create your own history files, set `SAVE_CSV` to `True` in `po_bot_indicators.py`. Or you can use any non-OTC assets available in yfinance to get history data.
