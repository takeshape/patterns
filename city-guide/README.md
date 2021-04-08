# City Guide

A simple IP-based city guide, providing weather and business data based on a provided
IP address.

<a href="https://app.takeshape.io/add-to-takeshape?repo=https://github.com/takeshape/patterns/tree/main/city-guide"><img alt="Deploy To TakeShape" src="https://camo.githubusercontent.com/1b580e3ce353d235bde0f376ca35b0fb26d685f3750a3013ae4b225dd3aaf344/68747470733a2f2f696d616765732e74616b6573686170652e696f2f32636363633832352d373062652d343331632d396261302d3130616233386563643361372f6465762f38653266376264612d306530382d346564652d613534362d3664663539626536613862622f4465706c6f79253230746f25323054616b65536861706525343032782e706e673f6175746f3d666f726d6174253243636f6d7072657373" width="205" height="38" data-canonical-src="https://images.takeshape.io/2cccc825-70be-431c-9ba0-10ab38ecd3a7/dev/8e2f7bda-0e08-4ede-a546-6df59be6a8bb/Deploy%20to%20TakeShape%402x.png?auto=format%2Ccompress" style="max-width:100%;"></a>

## Services

- [IP-API](https://ip-api.com/docs/api:json)
- [OpenWeather](https://openweathermap.org/current)
- [Yelp](https://www.yelp.com/developers/documentation/v3/get_started)

## Story

Using IP-API we first attempt to geolocate the user based on IP. If we were building
a real app and wanted more accurate data, we might even accept lat/lon coordinates
provided by a location API in the user's phone or browser. We parse this data to
get a zip code, then pass that to OpenWeatherMaps for information about the weather.
We also send the zip to Yelp for some suggested places to eat. We conform this to
a relatively simple GraphQL response, tailored to the use of the calling application.

## Query

IPs to try:

- `71.125.44.185` -> Brooklyn, NY
- `50.108.37.106` -> Muskegon, MI
- `128.218.229.26` -> San Francisco

```graphql
query GetLocation {
  getLocation(ip: "50.108.37.106") {
    location {
      city
      zip
    }
    weather {
      name
      weather {
        id
        main
        description
      }
    }
    business {
      name
      url
    }
  }
}
```
