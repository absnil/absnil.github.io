---
layout: post
title: "A dabble in Dynamic Charting of Stock Data using Dash"
date: 2019-08-28
---
So I spent an afternoon dabbling in [Dash by Plotly][dash-plotly] which helps in some really creative charting of stock market data. There is a pretty good article of this on [Medium][medium].
The article talks about a lot of fancy things you can do with the help of three pretty good dynamic plots.
I implemented a pretty simplified version of this [Here][here].
I also included in it the code to create the csv in the format required by Dash which is given above.
```
import pandas as pd
import numpy as np
from alpha_vantage.timeseries import TimeSeries

stock_list=['AMZN','TSLA','FB','AAPL']

main_df=pd.DataFrame()
for stock in stock_list:
    ts = TimeSeries(key= 'INSERT YOUR API KEY HERE', output_format='pandas',indexing_type='date')
    try:
        data, meta_data = ts.get_daily_adjusted(symbol=stock, outputsize='full')
        data = data.rename(index=str, columns={"1. open":"Open","2. high": "High", "3. low": "Low","4. close":"Close"})
        data['Symbol']=stock
        main_df=main_df.append(data)
    except:
        print("no data")

main_fin=main_df.filter(['Open','Close','Symbol'],axis=1)

main_fin.to_csv('stock_data1.csv'
```
The chart I made looks like this
![My helpful screenshot](/assets/img/screenshot_dash.png)
Got stock data using the collected using the Alphavantage API. There's a lot of scope and further work that can go with Dash. Go ahead and explore.


[dash-plotly]:https://plot.ly/dash/
[medium]:https://towardsdatascience.com/interactive-dashboards-for-data-science-51aa038279e5
[here]:https://github.com/absnil/dabble_in_dash
