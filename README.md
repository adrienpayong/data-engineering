# data-engineering

To navigate a data lake, a data catalog is typically provided. It abstracts the details of where to find the data and in what format it is stored. Some catalogs hold even more metadata.For developers, referencing a data catalog removes hardcoded parts from code. Generally you’re not interested in the details of loading the data, you just want to do useful things with it. A very simple data catalog, named catalog, has been prepared for you. It’s a Python dictionary mapping names of datasets to subclasses of DataLinks, a class that you will be unfamiliar with. In the real world, you will often come across classes that you haven’t encountered before. A DataLink is a custom class that simply encapsulates some metadata (like location, file type and presence of headers). Call the .read() method of the catalog’s diaper_reviews to retrieve the actual dataset (so not the metadata stored in the catalog) and inspect this returned object. What type is it?

Working with JSON

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
