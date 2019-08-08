# Description of the data:

Regarding the data to be used, the data science team has found the following sources:

### Public data bank of Madrid’s municipality
* Website: https://datos.madrid.es
* Data provided mainly in CSV or TXT files directly from the website or APIs if available.
* CSV and TXT can be imported to a dataframe using **Pandas** (https://pandas.pydata.org/) Python library.
* Data to be obtained: Districts (Nombre del distrito), neighborhoods(Nombre del barrio), postal codes(Codigo  Postal), geographical locations(Longitud, Latitud) and land value.

#### Example:
> data=pd.read_csv('https://datos.madrid.es/egob/catalogo/200075-1-callejero.csv', encoding='iso-8859-1', sep=';')  

### OpenStreetMap API
* Website: https://www.openstreetmap.org/
* Data provided using OpenStreetMap API.
* Geographical data can be extracted using **geopy.geocoders** library (https://geopy.readthedocs.io/).
* Data to be obtained: Geographical data of the districts, neighborhoods and postal codes.

#### Example:
> from geopy.geocoders import Nominatim  
> geolocator = Nominatim(user_agent="OpenStreetMaps")  
> geocode = RateLimiter(geolocator.geocode, min_delay_seconds=1)  
> df['Search'].apply(geocode)  

### Foursquare API
* Website: https://es.foursquare.com/developers/
* Data provided using Foursquare API.
* Foursquare API data can be turned to dataframes using **Pandas** (https://pandas.pydata.org/) and **Requests** (https://2.python-requests.org/en/master/) Python libraries.
* Data to be obtained: Services (Public transport, offices/business centers, hotels, restaurants…) and geographical data of the venues.

#### Example:
> url = 'https://api.foursquare.com/v2/venues/search?client_id={}&client_secret={}&ll={},{}&v={}&radius={}\  
> &limit={}'.format(CLIENT_ID, CLIENT_SECRET, neighborhood_latitude, neighborhood_longitude, VERSION, radius, LIMIT)  
> results = requests.get(url).json()  

### Preprocessing and data wrangling:
We need to see how to group the areas to join the data from Madrid’s municipality data bank. We can focus on districts, neighborhoods or postal codes depending on the availability of the data obtained.

Once we have a key to group the areas, we can start working in the acquisition of data from Foursquare API, filtering and counting the services or parameters defined by Company & Co.

We will need to obtain a complete dataframe with the following columns:

* Area: May be disctrict, neighborhood or postal code, depending on the data provided.
* Metro Stations: Number or relevance of metro stations in each area..
* Offices: Number or relevance of offices and/or business centers in each area.
* Hotels: Number or relevance of hotels in each area.
* Restaurants: Number or relevance of restaurants in each area.
* Land value: Estimated land value of the area.

Afterwards, we can cluster each neighborhood according to the data obtained. Apart from that, we will be able to weight each parameter if or plot the data in a map if necessary.
