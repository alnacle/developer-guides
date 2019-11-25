# Your first call in 2 minutes

## Step 1: Set up your account

The first step to start using Amadeus Self-Service APIs is to register and create an account:

* In the top right corner of the page, click on [register](https://developers.amadeus.com/register)
* Complete the form, using a valid email address and click on the `Create account` button. An automatic confirmation email will be sent to the email address you registered
* In the confirmation email you receive, click on `Confirm my account`

## Step 2: Get your API key

To start using the APIs you need to tell the system that you are allowed to do so. This process is called authentication.

All you need to do is to attach an alphanumeric string called **token** to your calls. This token will identify you as valid user and is generated from two parameters: `API Key` and `API Secret`.

{% hint style="success" %}
**Use your free calls in the test environment to create your app** 

In the test environment you will enjoy a fixed number of free API call quota per month for all your applications. When you reach the limit, you will receive an error message. Use this limited data collection to prototype your app and get ready for launching it to the market.
{% endhint %}

Getting the `API Key` and `API Secret` is easy. Once your account has been verified, you can [sign in](https://developers.amadeus.com/signin) and follow these steps:

* Click on your username \(top right corner\)
* Go to [My Self-Service Workspace](https://developers.amadeus.com/my-apps)
* Click on **Create New App** button
* Enter your application details and click on **Create**

## Step **3**: Make your first call

We recommend you use one of our [existing SDKs](https://github.com/amadeus4dev) available for Node, Java, Python and Ruby, but for this example we will use [cURL](https://curl.haxx.se/).

For our first call, let's get a list of possible destinations from Paris for a maximum amount of 200 EUR using the [Flight Inspiration Search API](https://developers.amadeus.com/self-service/category/203/api-doc/3/api-docs-and-example/10001), which returns a list of destinations from a given origin along with the cheapest price for each one.

Before making your first API call, you need to get your access token. For security purposes we implemented the `oauth2` process that will give you your access token based on your `API Key` and `API Secret`: please take a look at our [Authorization guide](https://developers.amadeus.com/self-service/apis-docs/guides/authorization).

The documentation says you need to use `v1/shopping/flight-destinations` as endpoint followed by the mandatory parameter `origin`. As you want to filter the offers to those cheaper than 200 EUR, you need to add the `maxPrice` parameter as well.

Our call is therefore:

```bash
curl 'https://test.api.amadeus.com/v1/shopping/flight-destinations?origin=PAR&maxPrice=200' \
      -H 'Authorization: Bearer {{token}}'
```

  


