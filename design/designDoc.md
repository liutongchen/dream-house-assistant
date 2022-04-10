## Table of Contents
- [Table of Contents](#table-of-contents)
- [Mock Up](#mock-up)
- [Data Points to Collect](#data-points-to-collect)
  - [Crime-related data points](#crime-related-data-points)
  - [Noise](#noise)
  - [Demographic](#demographic)
  - [Distance to Powerline](#distance-to-powerline)
  - [Average Income](#average-income)
  - [House Creep](#house-creep)
  - [Rent Price](#rent-price)

## Mock Up
![mockup](mockup.png)

## Data Points to Collect
### Crime-related data points
  
1. Given the latitude and longitude, return the crime score. [(Ref)](https://rapidapi.com/yourmapper/api/crimescore/) 

    Example Request:
    ```bash
    curl --request GET \
        --url 'https://crimescore.p.rapidapi.com/crimescore?lat=38.08809&lon=-85.679626&f=json&id=174' \
        --header 'X-RapidAPI-Host: crimescore.p.rapidapi.com' \
        --header 'X-RapidAPI-Key: 8250e38278msh93c58f0574456f1p168440jsn5404cf0da539'
    ```
    Example 200 Response:
    ```
    Not found
    ```
   
2. Given the latitude, longitude and distance, return the incidence details. [(Ref)](https://rapidapi.com/crimeometer/api/crimeometer/)

    Example Request:
    ```bash
        curl --request GET \
            --url 'https://crimeometer.p.rapidapi.comraw-data/?datetime_end=%3CREQUIRED%3E&lat=%3CREQUIRED%3E&datetime_ini=%3CREQUIRED%3E&lon=%3CREQUIRED%3E&distance=%3CREQUIRED%3E' \
            --header 'X-RapidAPI-Host: crimeometer.p.rapidapi.com' \
            --header 'X-RapidAPI-Key: 8250e38278msh93c58f0574456f1p168440jsn5404cf0da539' \
            --header 'x-api-key: k3RAzKN1Ag14xTPlculT39RZb38LGgsG8n27ZycG'
    ```

    Example 200 Response:
    ```json
    [
    {
        "total_incidents": 2,
        "total_pages": 1,
        "incidents": [
        {
            "city_key": "AUS",
            "incident_code": "20191101137",
            "incident_date": "2019-04-20T15:53:00.000Z",
            "incident_offense": "Driving Under the Influence",
            "incident_offense_code": "90D",
            "incident_offense_description": "Driving Under the Influence",
            "incident_offense_detail_description": "Driving Under the Influence at 5309 E RIVERSIDE DR",
            "incident_offense_crime_against": "Society",
            "incident_offense_action": "C",
            "incident_source_original_type": "DWI",
            "incident_source_name": "Austin_Police_Department_Crime_Reports",
            "incident_latitude": 30.2292141,
            "incident_longitude": -97.71322768,
            "incident_address": "5309 E RIVERSIDE DR"
        },
        {
            "city_key": "AUS",
            "incident_code": "20191101207",
            "incident_date": "2019-04-20T16:54:00.000Z",
            "incident_offense": "Assault Offenses",
            "incident_offense_code": "13A",
            "incident_offense_description": "Aggravated Assault",
            "incident_offense_detail_description": "Aggravated Assault at 5809 SWEENEY CIR",
            "incident_offense_crime_against": "Person",
            "incident_offense_action": "C",
            "incident_source_original_type": "AGG ASSAULT FAM/DATE VIOLENCE",
            "incident_source_name": "Austin_Police_Department_Crime_Reports",
            "incident_latitude": 30.30535921,
            "incident_longitude": -97.67908217,
            "incident_address": "5809 SWEENEY CIR"
        }
        ]
    }
    ]
    ```

Another API that returns similar data is [CrimeData](http`://rapidapi.com/jgentes/api/crime-data/).

Example Request:
```bash
    curl --request GET \`
        --url 'https://jgentes-crime-data-v1.p.rapidapi.com/crime?startdate=9%2F19%2F2015&enddate=9%2F25%2F2015&long=-122.5076392&lat=37.757815' \
        --header 'X-RapidAPI-Host: jgentes-Crime-Data-v1.p.rapidapi.com' \
        --header 'X-RapidAPI-Key: SIGN-UP-FOR-KEY'
```

Example Response:
```json
    [
        {
        "description":"HARASSING COMMUNICATIONS",
        "datetime":"6/24/2014 11:15 PM",
        "location":[42.343060293817736, -83.02064787655652]
        },
        {
            "description":"LARCENY - PERSONAL PROPERTY FROM VEHICLE",
            "datetime":"6/24/2014 08:15 PM",
            "location":[42.33607605681727, -83.05793091956167]
        }
    ]
```

### Noise
Given the latitude and longitude of a location, return the sound score. [(Ref)](https://howloud.com/developers/)

Example Request
```bash
    curl --request GET \`
        --url 'http://elb1.howloud.com/score?key=yourkey&longitude=-118&latitude=34' 
```

Example Response

```json
{
   "status":"OK",
   "request":{
      "latitude":“34.05615”,
      "key":"yourkey",
      "longitude":“-118.23596”
   },
   "result":[
      {
         "airports":0,
         "traffictext":"Busy",
         "localtext":"Active",
         "airportstext":"Calm",
         "score":68,
         "traffic":29,
         "scoretext":"Active",
         "local":2
      }
   ]
}
```

### Demographic
1. ServiceObjects API - given address, return age, income, race, gender information. [(ref)](https://www.serviceobjects.com/products-internal/demographics/demographics-data-plus/#) Pricing unknown.
2. Geocodio - given address, return census data include age, income, race, etc. 2,500 free lookups every day. [(ref)](https://www.geocod.io/docs/#demographics-census)
   
### Distance to Powerline
1. [Google Distance Matrix API](https://developers.google.com/maps/documentation/distance-matrix/overview) - calculate distance between origin and destination. The complexity of using this API is first fetching the exact location of nearby powerlines.
2. [EarthDefine API](https://buildings.earthdefine.com/) - Given the coordinate of an address, return the distance to the closest electrical powerline in meters, voltage of the closest powerline. Not sure about the pricing.

Example Request
```bash
GET https://api.buildings.earthdefine.com/v1/buildings?latitude=39.72&longitude=-105.1&token=80e4118a-045a-40db-8510-bf346064b0c9
```

Example Response
```
{
  "page": 0,
  "size": 10,
  "totalElements": 1749,
  "content": [
    {
      "systemScore": null,
      "score": null,
      "distance": 6.792244846145733,
      "distanceUnit": "METERS",
      "address": "200 Garrison St, Lakewood, CO 80226",
      "area": 2470,
      "city": "Lakewood",
      "county": "Jefferson County",
      "latitude": 39.719992255163696,
      "longitude": -105.09992122595098,
      "plusCode": "85FPPW92+X2W",
      "source": "Aerial Imagery",
      "sourceDate": "2017/09/02 00:00:00+00",
      "state": "CO",
      "zip": "80226",
      "geometry": "MULTIPOLYGON (((-105.099845433 39.7200249690001,-105.09984533 39.7199044980001,-105.099986585 39.7199044290001,-105.099986746 39.7200918280001,-105.099880805 39.72009188,-105.099880747 39.7200249520001,-105.099845433 39.7200249690001)))",
      "lineDistance": 1223.684187852931,
      "lineVoltage": 230,
      "lineVoltageClass": "220-287",
      "lineType": "AC",
      "lineStatus": "NOT AVAILABLE",
      "lineOwner": "NOT AVAILABLE"
    }
  ]
}
```

### House Creep
Not found

### Rent Price
1. [Zillow API](https://rapidapi.com/apimaker/api/zillow-com1/) - given the address, return the estimated rental price of a property

Example Request
```bash
curl --request GET \
	--url 'https://zillow-com1.p.rapidapi.com/rentEstimate?propertyType=%3CREQUIRED%3E&address=1093%20County%20Route%2060%2C%20Newton%20Falls' \
	--header 'X-RapidAPI-Host: zillow-com1.p.rapidapi.com' \
	--header 'X-RapidAPI-Key: 8250e38278msh93c58f0574456f1p168440jsn5404cf0da539'
```

Example Response
```json
{
  "comparableRentals":28,
  "percentile_25":1447.25,
  "highRent":1950,
  "lowRent":1214,
  "lat":44.200672,
  "median":1560.5,
  "rent":1699,
  "percentile_75":1599,
  "long":-74.990356,
}
```

2. [Rent Estimate API](https://rapidapi.com/moneals/api/rent-estimate) - given information of a property (e.g. address, # of rooms), return the estimated rental price.

Example Request
```bash
curl --request GET \
	--url 'https://realtymole-rental-estimate-v1.p.rapidapi.com/rentalPrice?propertyType=Single%20Family&address=5500%20Grand%20Lake%20Drive%2C%20San%20Antonio%2C%20TX&bathrooms=2&compCount=5&squareFootage=1600&bedrooms=4' \
	--header 'X-RapidAPI-Host: realtymole-rental-estimate-v1.p.rapidapi.com' \
	--header 'X-RapidAPI-Key: 8250e38278msh93c58f0574456f1p168440jsn5404cf0da5
```

Example Response
```json
{
  "rent":1434
  "rentRangeLow":1379.81
  "rentRangeHigh":1488.19
  "latitude":29.4759532
  "longitude":-98.35147909999999
  "listings":[{
      "address":"5114 Pond Lk"
      "bathrooms":"2"
      "bedrooms":4
      "city":"San Antonio"
      "county":"Bexar"
      "formattedAddress":"5114 Pond Lk, San Antonio, Texas 78244"
      "latitude":29.471978
      "longitude":-98.3509
      "photo":"https://ap.rdcpix.com/2062405879/642bca386732d79c6fff329322df786al-m0xd-w480_h480_q80.jpg"
      "price":1350
      "propertyType":"Single Family"
      "publishedDate":"2019-06-09T23:02:44.288Z"
      "squareFootage":1747
      "state":"TX"
      "zipcode":"78244"
      "distance":0.45
      "daysOld":26.74
      "correlation":0.9793
    }]
}
```

### Good APIs to investigate for phase two
* [Mashvisor API](https://rapidapi.com/mashvisor-team/api/mashvisor/) - given property, return investment analysis

## References
* [Real Estate APIs](https://rapidapi.com/blog/best-real-estate-apis/)
