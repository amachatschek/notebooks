---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.17.2
  kernelspec:
    display_name: WeatherPro
    language: python
    name: python3
---

<!-- #region editable=true slideshow={"slide_type": ""} -->
## **Open-Meteo API exploration - Historical Weather**
 
 ---
 
###  **Durchschnittstemperaturen PRO MONAT**

## **Für 1. Test: Jan. 2020 - Jan. 2025**
- API Request für mean temp. - daily
- "explore_json()"-ähnliche Helper-func schreiben
- pprint für Erste API-Begutachtung?
- Org. in list (**später** np-array)
- Speicherung in JSON (**Caching**)

#### *In der .env:* Default lat. + long., Default cache expire time, (normalerweise Key)
<!-- #endregion -->

```python
import requests
import requests_cache
from pprint import pp
from datetime import datetime
import json
import os
from dotenv import load_dotenv
```

```python
requests_cache.install_cache("temp_cache", expire_after=7200)
```

```python
api_url = "https://archive-api.open-meteo.com/v1/archive?latitude=51.414722&longitude=7.167222&start_date=2020-01-01&end_date=2025-01-01&daily=temperature_2m_mean&timezone=Europe%2FBerlin" #Winz-Baak, daily mean (täglicher Durchschnitt) Jan. 2020 - Jan. 2025

now = datetime.now()

def fetch_response(api_url):
    response = requests.get(api_url)
    response.raise_for_status()
    return response

response = fetch_response(api_url)
response_json = response.json() 
```

```python
def display_response(response_json):
    print(f"Response at {now.strftime("%x, %X")} : \n{response}")
    pp(response_json, indent=2, depth=2)
    return 

display_response(response_json)
```

```python


def zip_time_temp(response_json):
    time_tuple = tuple(response_json["daily"]["time"])
    temp_tuple = tuple(response_json["daily"]["temperature_2m_mean"])
    return tuple(zip(time_tuple, temp_tuple))


print(zip_time_temp(response_json)[:5])
```
