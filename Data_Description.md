# Data description:

Regarding the data to be used, the data science team has found the following sources:

### Public data bank of Madrid’s municipality
* Website: https://datos.madrid.es
* Data provided mainly in CSV or TXT files directly from the website.
* CSV and TXT can be imported to a dataframe using **Pandas** (https://pandas.pydata.org/) Python library.
* Data to be obtained: Districts (Nombre del distrito), neighborhoods(Nombre del barrio), postal codes(Codigo  Postal), geographical locations(Longitud, Latitud) and land value.

#### Example:
> data=pd.read_csv('https://datos.madrid.es/egob/catalogo/200075-1-callejero.csv', encoding='iso-8859-1', sep=';')  

### Foursquare API
* Website: https://es.foursquare.com/developers/
* Data provided using Foursquare API.
* Foursquare API data can be turned to dataframes using **Pandas** (https://pandas.pydata.org/) and **Requests** (https://2.python-requests.org/en/master/) Python libraries.
* Data to be obtained: Services (Public transport, offices/business centers, hotels, restaurants…) and geographical data of the venues.

#### Example:
>url = 'https://api.foursquare.com/v2/venues/search?client_id={}&client_secret={}&ll={},{}&v={}&radius={}&limit={}'.format(CLIENT_ID, CLIENT_SECRET, neighborhood_latitude, neighborhood_longitude, VERSION, radius, LIMIT)

### OpenStreetMap API
* Website: https://www.openstreetmap.org/
* Data provided using OpenStreetMap API.
* Geographical data can be extracted using **geopy.geocoders** library (https://geopy.readthedocs.io/).
* Data to be obtained: Geographical data of Madrid areas, neighborhoods or postal codes.

#### Example:
> import geocoder
> g = geocoder.osm('Nuevos Ministerios, Madrid')
> Longitude=g.x
> Latitude=g.y

## Preprocessing and data wrangling:
For this problem, we have decided to select the **neighborhood** as the minimal division of Madrid's urban area. There are in total 131 different administrative neighborhoods to be analysed.

We will get the data related to neighborhoods and geographical coordinates from the official Madrid's municipality data bank previously mentioned in **CSV** format. This data has the columns names in Spanish language and sometimes uses acronyms, so we will preprocess the data to get the columns in a readable English language in this case. 

The coordinates in the data of Madrid's data bank are given in WGS84 format. We will need to convert them to decimal format using libraries and some customized functions in Python, what generates some aditional tasks for the data wrangling. We will count on the **geocoder** library if it is necessary for this purpose.

Once we have the neighborhoods and coordinates are obtained, we can start working in the acquisition of data from **Foursquare API**. We will first get all the main venues for each neighborhood for clustering the neighborhoods later.
