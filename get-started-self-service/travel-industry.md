---
description: >-
  In this guide, we'll go over the full flight booking process, important points
  to consider when getting started and how to build a flight booking website or
  app using just three Amadeus APIs.
---

# Get started with flight booking

## How online booking works

Whether you want to create a flight booking website or app from scratch or add new features and possibilities in your app, flight booking is a powerful functionality that can boost your bottom line and give your users a complete end-to-end experience. Before you start building a flight booking website or app, it’s important to first understand how online booking works. Below, we’ll outline the overall booking flow and the role of each step in the process.

### Step 1: Perform a flight search

The first step in the online booking flow is a flight search. This returns a list of all available flights and fares for the desired search criteria.

### Step 2: Confirm availability and fare

The availability and price of airfare fluctuate so it’s important to confirm before proceeding to book. This is especially true if time passes between the initial search and the decision to book, as fares are limited and there are thousands of bookings occurring every minute. During this step, you can also add ancillary products like extra bags or legroom.

### Step 3: Make a booking

Once the fare is confirmed, you’re ready to book. In the airline industry, a booking is made when a Passenger Name Record \(PNR\) is created on the airline’s reservation system. A PNR is a unique record containing reservation data like passenger information and itinerary details.

### Step 4: Complete payment

Once the booking is made, you need to complete payment. In most cases, you’ll receive payment from the customer and then pay the airline, typically via an industry-specific settlement procedure like the BSP or ARC \(more on those later\).

### Step 5: Issue a ticket

In the final step, a flight ticket is issued. In industry terms, a flight ticket is a confirmation that payment has been received, the reservation has been logged, and the customer has the right to enjoy the flight. For [IATA member airlines](https://www.iata.org/about/members/Pages/airline-list.aspx), only certain accredited parties can issue tickets. In the next section, we’ll go into detail about your options for managing this final step in the booking process.

## How to issue a ticket

Most airlines only allow specially-licensed agents to issue tickets on their behalf. To issue a ticket, you must either contract with a host agency \(typically an airline consolidator\) to issue tickets for you or seek accreditation to issue the tickets yourself. Below, we’ll go over these **two main options** for issuing tickets:

### A. Issue tickets through an airline consolidator

Issuing tickets through an airline consolidator is the easiest way for small companies and travel newcomers to begin performing flight bookings. In this option, an airline consolidator serves as an accredited host agency and issues tickets on your behalf for a fee. 

#### **What is an airline consolidator?**

Airline consolidators are essentially flight ticket wholesalers that work directly with the airlines. They can issue tickets and often serve as hosts for travel agencies that are not accredited to issue tickets themselves.

Aside from issuing tickets, consolidators also usually offer post-ticketing services such as refunds or flight monitoring to detect schedule changes and cancellations.

Many start-ups and online travel companies prefer to issue tickets through an airline consolidator rather than seek accreditation. To do this, you must sign a contract with the consolidators in your desired markets. 

#### **What is the right airline consolidator for you?**

There are many airline consolidators throughout the world and finding the right one depends largely on your needs and location. [Contact us here](https://developers.amadeus.com/support/contact-us-self-service) and we will help you find the one that’s best for you.

### B. Get accredited to issue tickets yourself

To be able to issue tickets yourself, you must first become an accredited agent. This lets you issue tickets and avoid the fees charged by airline consolidators, though you may still wish to contract a consolidator for post-ticketing services.

Various airline associations provide accreditation to travel agencies. This accreditation lets you issue tickets on behalf the associated carriers and access the payment settlement services which must be used to pay the airlines. The two major accrediting organizations are:

* **International Air Transport Association \(IATA\)** – IATA is an association of 290 international airlines which, among other functions, provides booking and ticketing accreditation to travel agencies and provides payment settlement services through the Billing and Settlement Plan \(BSP\). Companies registered outside of the U.S. must have IATA accreditation to issue tickets and access the BSP. You can find more information on requirements and how to apply for accreditation on the [IATA website](https://www.iata.org/services/accreditation/accreditation-travel/Pages/application.aspx). 
* **Airlines Reporting Corporation \(ARC\)** – The ARC is company owned by various North American airlines that provides payment settlement services between airlines and retailers in the U.S. Travel agencies registered in the U.S. must have ARC accreditation to book, issue and fulfil flight tickets directly. Information on eligibility, requirements applying for ARC accreditation can be found on the [ARC website](https://www2.arccorp.com/products-participation/travel-agencies/become-an-arc-accredited-agent/).

{% hint style="warning" %}
**Note: local regulations may apply**

In some areas like California or France, managing flight bookings is subject to local regulations. If you’re unsure about what your local regulations are,
{% endhint %}

## How to build a booking engine with Amadeus APIs

With Amadeus APIs, it’s easy to create your own flight booking engine. Once you’ve decided how you want to issue tickets, you just need to use the following APIs to complete the booking process:

### Flight Offers Search API - retrieve a list of flights

he Flight Offers Search API starts the booking cycle with a search for the best fares. The API returns a list of the cheapest flights given a city/airport of departure, a city/airport of arrival, the number and type of passengers and travel dates. The results are complete with airline name and fares as well as additional information like bag allowance and pricing for additional baggage. Visit the [Flight Offers Search documentation page](https://developers.amadeus.com/self-service/category/air/api-doc/flight-offers-search) for more details on this API.

### Flight Offer Search API - confirm availability and get fare details

Once a flight has been selected, you’ll need to confirm the availability and price of the fare. This is where the Flight Offers Price API comes in. This API returns the final fare price \(including taxes and fees\) of flights from the Flight Offers Search API as well as pricing for ancillary products and the payment information that will be needed to make the final booking. Visit the [Flight Offers Price documentation page](https://developers.amadeus.com/self-service/category/air/api-doc/flight-offers-price) for more details on this API.

### Flight Create Orders API - book the flight

Once the fare is confirmed, you’re ready to use the Flight Create Orders API to perform the actual booking. This API lets you log a reservation in the airlines’ systems and create a PNR, and returns a unique ID number and the reservation details. If you’re using an airline consolidator, the PNR will be automatically sent to the consolidator for ticket issuance. [Visit the Flight Create Orders documentation page](https://developers.amadeus.com/self-service/category/air/api-doc/flight-create-orders) for more details on this API.

Remember, you need to be able to issue a ticket to make bookings with our Flight Create Order API. To access the API in production, you need to either sign a contract with an airline consolidator or be accredited to issue tickets yourself. Please [contact us](https://developers.amadeus.com/support/contact-us-self-service) to learn more about which options is best for you.

{% hint style="info" %}
## Summary

To conclude, flight booking is a powerful capability that you can easily incorporate into your business with Amadeus APIs. Follow these steps and get started building your booking engine today:

* **Perform a flight search** with our [Flight Offers Search API](https://developers.amadeus.com/self-service/category/air/api-doc/flight-offers-search)
* **Confirm the fare** with our [Flight Offers Price API](https://developers.amadeus.com/self-service/category/air/api-doc/flight-offers-price)
* **Make a booking** with our [Flight Create Orders API](https://developers.amadeus.com/self-service/category/air/api-doc/flight-create-orders)
* **Complete payment via an airline consolidator** or industry settlement plan
* **Issue a ticket through an airline consolidator** or get accredited to issue tickets yourself
{% endhint %}

