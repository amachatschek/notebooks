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
    display_name: Python (weatherpro)
    language: python
    name: weatherpro
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
import json
import os
from dotenv import load_dotenv
```

```python
requests_cache.install_cache("temp_cache", expire_after=3600)
```

```python
api_url = "https://archive-api.open-meteo.com/v1/archive?latitude=51.414722&longitude=7.167222&start_date=2020-01-01&end_date=2025-01-01&daily=temperature_2m_mean&timezone=Europe%2FBerlin" #Winz-Baak, daily mean (täglicher Durchschnitt) Jan. 2020 - Jan. 2025
response = requests.get(api_url, 

```
