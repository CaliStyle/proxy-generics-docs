---
title: Proxy Generics Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/CaliStyle/trailpack-proxy-engine'>Proxy Engine</a>

includes:
  - errors

search: true
---

# Introduction
Welcome to the Proxy Generics for Proxy Engine Docs! [Proxy Engine](https://github.com/CaliStyle/trailpack-proxy-engine) is an Open Source Node.js Framework created by the team at [Cali Style Technologies](https://cali-style.com).

## What are Proxy Generics?

Generics are common features that web applications need but implement differently. The result of a Generic is a normalized way of handling these different services.

A generic is a great way to implement 3rd parties. You can write your application to implement a single service but easily swap out the the 3rd party.

Generics can add their own Models, Controllers, Services, and Policies so they can support things like vendor specific webhooks or extend functionality.

## Current Generics
- Email Provider
- Payment Processors
- Tax Provider
- Shipping Provider
- Fulfillment Provider
- Geolocation
- Image Manipulation
- HTML rendering
- whatever you need!

Can you think of a generic or method we missed? Create a PR!

# Installation
To install Proxy Generics:

<code>
$ npm install trailpack-proxy-generics
</code>

If you are using Trail's yo generator:

<code>
$ yo trails:trailpack trailpack-proxy-generics
</code>

# Configuration
To configure Proxy Generics is simple, there are only 2 files to create/modify:

## config/main.js
> config/main.js

```javascript
module.exports = {
  packs: [
    // ... other trailpacks
    require('trailpack-proxy-generics')
    // ... other proxy-packs
  ]
}
```
Like all Trails' trailpacks, it must be included in the `config/main.js` file.

## config/proxyGenerics.js
> config/proxyGenerics.js

```javascript
module.exports = {
  // ... any generic
  payment_processor: {
      adapter: require('<adapter>'),
      options: {
          whatever_key: '<what ever you need here>'
      },
      api: require('<adapter>/api')
  }
}
```
Also, Proxy Generics takes it's own config in the `config/proxyGenerics.js` file.


### Config Parameters

Parameter | Type | Default | Description
--------- | ---- | ------- | -----------


## Usage
Many different modules in Proxy Engine will rely on a generic to complete a task. Generics are easy to create and use.

### Validation
Every Generic call is validated twice: 

- When data is passed to the generic.
- When there is a successful response from the generic.

This allows for generics to stay consistent with their requests and responses.

<aside class="success">
NOTE:
If a an instance of a model is passed to the generic, then the generic must mutate it return the same instance.
</aside>

# Email Provider
The Email Provider handles sending emails from different email providers eg. Mandrill, MailGun.

## EmailGenericService.send
Sends an Email

## EmailGenericService.sendTemplate
Sends an Email Template

## Creating an Email Provider Generic

## Supported Email Providers
* [Mandrill](https://github.com/CaliStyle/proxy-generics-mandrill)

# Geolocation Provider
The Geolocation Provider handles resolving geographical locations.

## GeolocationGenericService.locate
Resolves the geolocation of an address, validates an address, normalizes an address.

## Creating a Geolocation Provider Generic

```
TODO
```

# Tag Provider
The Tax Provider handles sales tax for items sold from different tax providers eg. TaxBundle

## TaxGenericService.getRate
Gets the tax rate for a purchase transaction.

## Creating a Tax Provider Generic
```
TODO EXAMPLE
```

## Supported Tax Providers
* [Taxjar](https://github.com/CaliStyle/proxy-generics-taxjar)

# Shipping Provider
The Shipping Provider handles shipping rates from a location to a destination from different shipping providers eg. Shipstation, USPS, FedEx, UPS.

### Shipping Provider (TODO)
The Shipping Provider handles shipping rates from a location to a destination from different shipping providers eg. Shipstation, USPS, FedEx, UPS

## ShippingGenericService.getRate
Gets a single carrier rate.

## ShippingGenericService.getRates
Gets all carrier rates

## Creating a Shipping Provider Generic
```
TODO EXAMPLE
```

# Fulfillment Provider
The Fulfillment Provider handles fulfillment events from a location to a destination from different fulfillment providers eg. Shipstation, Amazon, Custom

## FulfillmentGenericService.createOrder
Creates an order in fulfillment

## FulfillmentGenericService.createOrders
Creates multiple orders in fulfillment

## FulfillmentGenericService.updateOrder
Updates an order in fulfillment

## FulfillmentGenericService.updateOrders
Updates multiple orders in fulfillment

## FulfillmentGenericService.destroyOrder
Destroys an order in fulfillment

## FulfillmentGenericService.destroyOrders
Destroys multiple orders in fulfillment

## FulfillmentGenericService.getOrder
Retrieves an order in fulfillment

## FulfillmentGenericService.getOrders
Retrieves multiple orders in fulfillment

## FulfillmentGenericService.holdOrder
Creates an order hold in fulfillment

## FulfillmentGenericService.holdOrders
Creates multiple order holds in fulfillment

## Creating a Fulfillment Provider Generic
```
TODO EXAMPLE
```

## Supported Fulfillment Providers
* [Shippo](https://github.com/CaliStyle/proxy-generics-shippo)
* [Shipstation](https://github.com/CaliStyle/proxy-generics-shipstation)

# Payment Processor
The Payment Processor handles payments from different merchant processors/terminals eg. Stripe, Authorize.net.

## PaymentGenericService.authorize
Authorizes a purchase transaction

## PaymentGenericService.capture
Captures an authorized purchase transaction

## PaymentGenericService.sale
Authorizes and captures a purchase transaction

## PaymentGenericService.void
Voids an authorized purchase transaction

## PaymentGenericService.refund
Partially Refunds/Refunds a purchase transaction

## PaymentGenericService.createCustomer
Create a Customer Account

## PaymentGenericService.updateCustomer
Update a Customer Account

## PaymentGenericService.findCustomer
Find a Created Customer Account

## PaymentGenericService.getCustomerSources
Get Customer Sources (Payment Methods)

## PaymentGenericService.createCustomerSource
Create Customer Source (Payment Methods)

## PaymentGenericService.updateCustomerSource
Update Customer Source (Payment Methods)

## PaymentGenericService.findCustomerSource
Find a Customer Source (Payment Methods)

## PaymentGenericService.removeCustomerSource
Remove a Customer Source (Payment Methods)

## Creating a Payment Processor Generic
TODO EXAMPLE

## Supported Payment Processors
* [Stripe](https://github.com/CaliStyle/proxy-generics-stripe)
* [Authorize.net](https://github.com/CaliStyle/proxy-generics-authorize-net)

# Data Store Provider
The Data Store provider handles uploads and downloads to a remote data store eg. AWS, gCloud, and some permissions.

## DataStoreGenericService.upload
Uploads a buffer to a data store

## DataStoreGenericService.uploadFile
Uploads a file to a data store

## DataStoreGenericService.uploadFiles
Uploads files to a data store

## Creating a Data Store Provider Plugin
```
TODO EXAMPLE
```


# Image Provider
Handles image manipulation.

## Creating an Image Provider Plugin
```
TODO EXAMPLE
```

# Render Provider
Handles rendering of html and Metadata

```javascript
{
    document: '<h1>Hello World</h1>'
    meta: {
      key: 'Look at Me!'
    }
}
```
## RenderGenericService.render
Renders markdown/html string asynchronously.

## RenderGenericService.renderSync
Renders markdown/html string synchronously.

## Creating a Render Service Plugin
```javascript
TODO EXAMPLE
```

#### Supported Render Services
* [Render](https://github.com/CaliStyle/proxy-generics-render)

[ci-sequelize-image]: https://img.shields.io/travis/trailsjs/trailpack-proxy-sequelize/master.svg?style=flat-square
[ci-sequelize-url]: https://travis-ci.org/trailsjs/trailpack-proxy-sequelize

[ci-express-image]: https://img.shields.io/travis/trailsjs/trailpack-express/master.svg?style=flat-square
[ci-express-url]: https://travis-ci.org/trailsjs/trailpack-express
