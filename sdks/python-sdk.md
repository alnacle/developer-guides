---
description: >-
  Create custom Amadeus for Developers based applications using our Python
  library.
---

# Python SDK

## Installation

This SDK requires Python 2.7+ or 3.4+. You can install it directly with pip.

.. code:: sh

```text
pip install amadeus
```

You can also add it to your `requirements.txt` file and install using:

.. code:: sh

```text
pip install -r requirements.txt
```

## Getting Started

To make your first API call you will need to `register for an Amadeus Developer Account <https://developers.amadeus.com/create-account>`\_\_ and set up your first application.

.. code:: py

```text
from amadeus import Client, ResponseError

amadeus = Client(
    client_id='REPLACE_BY_YOUR_API_KEY',
    client_secret='REPLACE_BY_YOUR_API_SECRET'
)

try:
    response = amadeus.reference_data.urls.checkin_links.get(airlineCode='BA')
    print(response.data)
except ResponseError as error:
    print(error)
```

### Initialization

The client can be initialized directly.

.. code:: py

```text
# Initialize using parameters
amadeus = Client(client_id='REPLACE_BY_YOUR_API_KEY', client_secret='REPLACE_BY_YOUR_API_SECRET')
```

Alternatively it can be initialized without any parameters if the environment variables `AMADEUS_CLIENT_ID` and `AMADEUS_CLIENT_SECRET` are present.

.. code:: py

```text
amadeus = Client()
```

Your credentials can be found on the `Amadeus dashboard <https://developers.amadeus.com/my-apps/>`**. `Sign up <https://developers.amadeus.com>`** for an account today.

By default the environment for the SDK is the `test` environment. To switch to a production \(paid-for\) environment please switch the hostname as follows:

.. code:: py

```text
amadeus = Client(hostname='production')
```

## Documentation

Amadeus has a large set of APIs, and our documentation is here to get you started today. Head over to our `Reference <https://amadeus4dev.github.io/amadeus-python/>`\_\_ documentation for in-depth information about every SDK method, its arguments and return types.

* `Initialize the SDK <https://amadeus4dev.github.io/amadeus-python/#/client>`\_\_
* `Find an Airport <https://amadeus4dev.github.io/amadeus-python/#referencedata-locations>`\_\_
* `Find a Flight <https://amadeus4dev.github.io/amadeus-python/#shopping-flights>`\_\_
* `Get Flight Inspiration <https://amadeus4dev.github.io/amadeus-python/#shopping-flights>`\_\_

## Making API calls

This library conveniently maps every API path to a similar path.

For example, `GET /v2/reference-data/urls/checkin-links?airlineCode=BA` would be:

```text
amadeus.reference_data.urls.checkin_links.get(airlineCode='BA')
```

Similarly, to select a resource by ID, you can pass in the ID to the singular path.

For example, `GET /v2/shopping/hotel-offers/XZY` would be:

```text
amadeus.shopping.hotel_offer('4BA070CE929E135B3268A9F2D0C51E9D4A6CF318BA10485322FA2C7E78C7852E').get()
```

You can make any arbitrary API call as well directly with the `.get` method:

```text
amadeus.get('/v2/reference-data/urls/checkin-links', airlineCode='BA')
```

Or with `POST` using `.client.post` method:

```text
amadeus.post('/v1/shopping/flight-offers/pricing', body)
```

### Response

Every API call returns a `Response` object. If the API call contained a JSON response it will parse the JSON into the `.result` attribute. If this data also contains a `data` key, it will make that available as the `.data` attribute. The raw body of the response is always available as the `.body` attribute.

.. code:: py

```text
from amadeus import Location

response = amadeus.reference_data.locations.get(
    keyword='LON',
    subType=Location.ANY
)

print(response.body) #=> The raw response, as a string
print(response.result) #=> The body parsed as JSON, if the result was parsable
print(response.data) #=> The list of locations, extracted from the JSON
```

### Pagination

If an API endpoint supports pagination, the other pages are available under the `.next`, `.previous`, `.last` and `.first` methods.

```text
from amadeus import Location

response = amadeus.reference_data.locations.get(
    keyword='LON',
    subType=Location.ANY
)

amadeus.next(response) #=> returns a new response for the next page
```

If a page is not available, the method will return `None`.

### Logging & Debugging

The SDK makes it easy to add your own logger.

```text
import logging

logger = logging.getLogger('your_logger')
logger.setLevel(logging.DEBUG)

amadeus = Client(
    client_id='REPLACE_BY_YOUR_API_KEY',
    client_secret='REPLACE_BY_YOUR_API_SECRET',
    logger=logger
)
```

Additionally, to enable more verbose logging, you can set the appropriate level on your own logger, though the easiest way would be to enable debugging via a parameter on initialization, or using the `AMADEUS_LOG_LEVEL` environment variable.

```text
amadeus = Client(
    client_id='REPLACE_BY_YOUR_API_KEY',
    client_secret='REPLACE_BY_YOUR_API_SECRET',
    log_level='debug'
)
```

