# reading JSON  Data from  API 
```python

import csv
from datetime import datetime

import requests
from urllib3.filepost import writer

url='https://a6bbcd99-cf64-4c56-a4d8-ba4d940e57b8.mock.pstmn.io/events.json'

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

data= requests.get(url).json()
#print(data)
time_data={}

for row in data:
    timestamp = row.get('timestamp')
    dt= datetime.strptime(timestamp,'%Y-%m-%d %H:%M:%S')
    hour = dt.hour

    if hour not in time_data:      #intialization
        time_data[hour] = {
            'impressions':0,
            'clicks':0,
            'revenue':0,
            'conversion':0
        }

    time_data[hour]['impressions'] += int(row.get('impressions'))
    time_data[hour]['clicks'] += int(row.get('clicks'))
    time_data[hour]['revenue'] +=float(row.get('revenue'))
    time_data[hour]['conversion'] += int(row.get('conversion'))


print(time_data)

rows=[]
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

for hr, agg in time_data.items():
    impressions = agg['impressions']
    clicks = agg['clicks']
    conversions = agg['conversion']
    revenue = agg['revenue']

    row=    {
            'hour': hr,
            'impressions':impressions,
            'clicks':clicks,
            'conversion':conversions,
            'revenue':revenue,
            'click_through_rate': clicks / impressions,
            'conversion_rate':conversions / impressions,
            'revenue_per_impression': revenue / impressions

        }

    rows.append(row)



with open('result.csv', mode='w', newline='') as file:
    writer=csv.DictWriter(file, fieldnames=fields)
    writer.writeheader()
    writer.writerows(rows)



# select
# d.compaign_name,
# sum(f.revenue) as total_revenue
# from fact_event as f join dim_compaign as d on f.compaign_id = d.compaign_id
# group by d.compaign_name
# having sum(f.revenue) > 1000000

```
# order by sum(f.revenue) desc

