# reading JSON  Data from  API 
```python
import requests
import datetime

url = 'https://a6bbcd99-cf64-4c56-a4d8-ba4d940e57b8.mock.pstmn.io/events.json'
data = requests.get(url).json()

"""
hour
impressions
clicks
conversion
revenue
click_through_rate
conversion_rate
revenue_per_impression
"""

hourly_data = {}

for row in data:
    timestamp =row.get("timestamp")
    dt = datetime.datetime.strptime(timestamp, "%Y-%m-%d %H:%M:%S")
    hr = dt.hour

    if hr not in hourly_data:
        hourly_data[hr] =  {
            'impressions' : 0,
            'revenue': 0,
            'clicks': 0,
            'conversion': 0
        }

    hourly_data[hr]['impressions'] += int(row.get('impressions'))
    hourly_data[hr]['revenue'] += float(row.get('revenue'))
    hourly_data[hr]['clicks'] += int(row.get('clicks'))
    hourly_data[hr]['conversion'] += int(row.get('conversion'))


rows = []
fields=[
'hour',
'impressions',
'clicks',
'conversion',
'revenue',
'click_through_rate',
'conversion_rate',
'revenue_per_impression'
]

for hr, agg in hourly_data.items():
    impression = agg['impressions'],
    revenue = agg['revenue'],
    clicks = agg['clicks'],
    conversion = agg['conversion'],

    row = {
        'hour' : hr,
        'impressions' : impression,
        'revenue' : revenue ,
        'clicks' : clicks ,
        'conversion' : conversion,
        'click_through_rate' : clicks / impression,
        'conversion_rate': conversion / impression ,
        'revenue_per_impression': revenue / impression
    }
    rows.append(row)

print(row)

```



