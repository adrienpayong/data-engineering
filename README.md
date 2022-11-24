# data-engineering

To navigate a data lake, a data catalog is typically provided. It abstracts the details of where to find the data and in what format it is stored. Some catalogs hold even more metadata.For developers, referencing a data catalog removes hardcoded parts from code. Generally you’re not interested in the details of loading the data, you just want to do useful things with it. A very simple data catalog, named catalog, has been prepared for you. It’s a Python dictionary mapping names of datasets to subclasses of DataLinks, a class that you will be unfamiliar with. In the real world, you will often come across classes that you haven’t encountered before. A DataLink is a custom class that simply encapsulates some metadata (like location, file type and presence of headers). Call the .read() method of the catalog’s diaper_reviews to retrieve the actual dataset (so not the metadata stored in the catalog) and inspect this returned object. What type is it?

## Working with JSON

Because JSON is ubiquitous, you should be able to read and write this format. As you will see in the next lesson, many configuration files in Singer hold JSON.
In this exercise, you will write some configuration details of a database to a JSON file. Doing this is good practice by the way, as it keeps hardcoded parts out of your code, which allows other people to reference the same configuration files using other languages even. Do not hesitate to refer to the slides, available in the tab on the right of IPython Shell, if you’re stuck.
```
# Import json
import json

database_address = {
  "host": "10.0.0.5",
  "port": 8456
}

# Open the configuration file in writable mode
with open("database_config.json", "w") as fh:
  # Serialize the object in this file handle
  json.dump(obj=database_address, fp=fh)
  
  ```
  
  ## Specifying the schema of the data

You’re given a dataset of pricing details of diapers from several stores. After some inspection, you understand that the products have an identical schema, regardless of the store. Since your company is already invested in Stitch, the mother company of Singer, you’ll be writing a custom Singer “tap” to export the different products in a standardized way. To do so, you will need to associate a schema with the actual data.
```
schema = {'properties': {
    'brand': {'type': 'string'},
    'model': {'type': 'string'},
    'price': {'type': 'number'},
    'currency': {'type': 'string'},
    'quantity': {'type': 'number', 'minimum': 1},  
    'date': {'type': 'string', 'format': 'date'},
    'countrycode': {'type': 'string', 'pattern': "^[A-Z]{2}$"}, 
    'store_name': {'type': 'string'}}}

# Write the schema
singer.write_schema(stream_name='products', schema=schema, key_properties=[])
```
## Running an ingestion pipeline with Singer

## Communicating with an API

The marketing team you are collaborating with has been scraping several websites for customer reviews on consumer products. The dataset is only exposed to you through an internal REST API. You would like to add that data in its entirety to the data lake and store it in a convenient way, say csv. While the data is available over the company’s internal network, you still need to supply the API key that the marketing team has created for your exploration use case: api_key: scientist007.
For technical reasons, the endpoint has been made available to you on localhost:5000. You can “browse” to it, using the well-known requests module, by calling requests.get(SOME_URL). You can authenticate to the API using your API key. Simply fill in the template URL <endpoint>/<api_key>/.
  
  endpoint = "http://localhost:5000"
```
# Fill in the correct API key
api_key = "scientist007"

# Create the web API’s URL
authenticated_endpoint = "{}/{}".format(endpoint, api_key)

# Get the web API’s reply to the endpoint
api_response = requests.get(authenticated_endpoint).json()
pprint.pprint(api_response)
```
