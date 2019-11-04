# Streaming data via OIC into BigQuery

![](/OIC2/30.jpg)

## Introduction

Oracle Integration can abstract away complex authentication protocols for your app developers. Instead of having your develpers implement OAuth2 protocols in their applications to call the BigQuery API - OIC can take care of it and you can provide your develpers their OIC service account Basic Auth credentials and the endpoint. 

This is a continuation of [this lab.](https://github.com/GaryHostt/BigQueryIntegration/blob/master/README.md)
Click here to learn more about [Oracle Integration.](https://cloud.oracle.com/OIC)
Click here to learn more about [Streaming data into BigQuery.](https://cloud.google.com/bigquery/streaming-data-into-bigquery#bigquery_table_insert_rows-csharp)

## Objectives

•	Stream data into BigQuery via OIC

### Outline
1. Create an app driven integration
2. Configure a Python script to call the REST endpoint
3. Run the data loading script
5. Monitor the integration 

## Reference

![](OIC/32.png)

This is also how your integration will look at the end of the walkthrough.

During the walkthrough, relevant instructions will be UNDER the picture they correlate with.

Below is the python script file we will be using, you will configure the authorization header and url to work with your OIC environment:

```
import json
import random
import datetime
import time
import requests
from requests.exceptions import HTTPError
from datetime import datetime
import http.client
from random import randint, choice

#static values
WH_ID = ['WH1', 'WH2', 'WH3', 'WH4', 'WH5', 'WH6', 'WH7']
Item_name = ['Mechanically Separated', 'Shelf-Stable, Pathogen Negative Meat Slurry', 'Poultry Fat', 'Chicken Meal', 'Whole Ground']

def createJSON():
    data = {}
    data['WH_ID'] = random.choice(WH_ID)
    data['Item_Name'] = random.choice(Item_name)
    data['Item_id'] = random.randint(100, 110)
    data['Quantity_Available'] = random.randint(1000, 5000)
    data['Quantity_Requested'] = random.randint(1000, 5000)
    data['Backlog'] = random.randint(1000, 5000)
    return data
# Generate each parameter's data input in varying proportions
def submitData(data):
    headers = {
        'Content-Type': "application/json",
        'Content-Transfer-Encoding': "buffered",
        'Authorization': "FROM POSTMAN"
            }
    payload = data
    print(payload)  
    url='YOUR OIC URL'
    r = requests.request("POST", url, data=payload, headers=headers)
    print(r.status_code)
    response = requests.Session()
# Send payload to OIC

#Performs functions
while True:
    time.sleep(1)
    rnd = random.random()
    #$print(rnd)
    if (0 <= rnd < 0.99):
        data = json.dumps(createJSON())
        submitData(data)
        print('data submitted')
    elif (0.99<= rnd < 1):
        pass
```

# Walkthrough

## 1.	Create an app driven integration

![](/OIC2/1.png)
![](/OIC2/2.png)
![](/OIC2/3.png)
![](/OIC2/4.png)
![](/OIC2/5.png)
![](/OIC2/6.png)
![](/OIC2/7.png)
![](/OIC2/8.png)
![](/OIC2/9.png)
![](/OIC2/10.png)
![](/OIC2/11.png)
![](/OIC2/12.png)
![](/OIC2/13.png)
![](/OIC2/14.png)
![](/OIC2/15.png)
![](/OIC2/16.png)
![](/OIC2/17.png)
![](/OIC2/18.png)
![](/OIC2/19.png)
![](/OIC2/20.png)
![](/OIC2/21.png)

From your Google Cloud console, click the menu on the left and under Big Data, click BigQuery. 

## 2. Configure a Python script to call the REST endpoint
![](/OIC2/23.png)
![](/OIC2/24.png)

![](/OIC2/24a.png)
![](/OIC2/25.png)
## 3. Run the data loading script
## 4. Monitor the integration 

![](/OIC2/28.png)



