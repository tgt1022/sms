# Intelecom SMS Gateway
## Official documentation

Welcome to the developer pages for the Intelecom SMS Gateway API. Here you will find all you need to SMS-enable your applications. This repository will cover the general API documentation and code samples. In addition we provide several other repositories containing finished libraries for many different programming languages.

### Where to start?

Well - that depends on you, may we suggest:

- Browsing our [list of libraries](#list-of-official-libraries) you can import into your existing code - A good choice if you want to just dive right into coding.
- Learn how our documentation is [structured](#how-the-documentation-is-structured)
- Read our [introduction to A2P SMS and SMS Gateways](sections/about.md) - a good starting point if you have not used a SMS Gateway before.
- Read the [API documentation](/sections/interfaces-general.md) for one of our specific interfaces
- [Learn about Intelecom](#about-intelecom), our history in providing SMS services and other related products.
- Find out [how to register an account](#registering-an-account) with Intelecom to start using the SMS Gateway services.

### List of official libraries

We provide you with many "off-the-shelf" libraries that you may use directly in your existing or new applications. Feel free to expand, modify and improve these libraries and we would be thrilled if you send us a pull request or two.

These links will navigate to the respective repository for the chosen library. Basic information about how to get started using these libraries are provided, but please refer to these pages for more in-detail information about the APIs.

**List of current libraries:**

- [PHP](https://github.com/Intelecom/smsgw-client-php)  
- [Java](https://github.com/Intelecom/smsgw-client-java) 
- [.NET](https://github.com/Intelecom/smsgw-client-dotnet)  
- [Go](https://github.com/Intelecom/smsgw-client-go)  
- [Python](https://github.com/Intelecom/smsgw-client-python)  
- [Node.js](https://github.com/Intelecom/smsgw-client-nodejs)   

Please do get in touch and let us know if you are missing any libraries from this list.

### How the documentation is structured

The documentation consists of different sections, starting with an overview / table of contents page. From each section you may navigate to the next section, or jump directly into a specific section.

**Section list:**

- [Overview](sections/overview.md) (Introduction and ToC)
- [About A2P SMS and SMS Gateways](sections/about.md)
- [Common SMS Gateway documentation](sections/common.md) - information relevant to most of the interfaces.
- [Interface specifications](sections/interfaces-general.md)
	- [REST API](sections/interfaces/rest.md)
	- [SOAP API](sections/interfaces/soap.md)
	- [HTTP GET API](sections/interfaces/http-get.md)
	- [SMTP SMS GW](sections/interfaces/smtp.md)
	- [TCP sockets / XML API](sections/interfaces/tcp-xml.md)
	- [SMPP](sections/interfaces/smpp.md)
	- [Management API](sections/interfaces/management-api.md)
	- [Value-added services for MO messages](sections/interfaces/vas.md)
- Library documentation - [Each library](#list-of-official-libraries) provides a basic "getting started" in each repo (readme.md).
- How to [get in touch with us](sections/contact.md)?

We also provide reference documentation such as the SMPP specification and GSM specifications. 

### Registering an account

To use the SMS Gateway you will need the URLs to our staging / production sites as well as some credentials:

- Username 
- Password
- Serviceid


If you do not already have an account and want to try out or order access, please do [contact us](sections/contact.md) for more information. We provide demo accounts for both live and emulated MNOs - no strings attached. 

For live accounts pricing is based on establishment, monthly subscription and traffic (per message) fees. 


### About Intelecom 

Intelecom is a leading provider of cloud-based and on-premise communication solutions. We have over 30 years of experience and with our experience and competence we aim to give our customers stable, flexible, user-friendly and scalable solutions. 

We provide innovative solutions for SMS, mobile applications, system integration, call-centers, wireless networks, unified communications and more. Our customer base counts over 2000 customers across many verticals from offshore to transport, primarily in Scandinavia and UK. What most of our customers have in common is that they have a need to be able to communicate better with their users and employees. Our contribution is often that we offer means to integrate existing solutions with new ones or new interfaces. This results in continuous utilization of current investments and at the same time providing additional value for the customer. Our mission is to make sure that good communication is rewarding. 

SMS solutions have been a part of Intelecom starting with the platform originally set up by Carrot Communications back in 2000. Since then not a lot have changed in the basic SMS GSM specifications, but a lot have changed concerning our customers' demands for stability, scalability, redundancy and speed. SMS now is a business critical application for many companies, both private and public. In addition, a lot has happened with SMS as a payment channel over the years. In later years many telcos have been opening up for selling physical goods and services, using SMS or carrier billing as payment. We at Intelecom have been working hard to keep up, both with customer demands and new possibilities over the years. As a result, we have a SMS platform, now in it's fifth major version, that is both technically advanced, high-capacity and stable. 

#### Intelecom Group
[Intelecom Group AS](http://www.intelecom.no) was started in Norway in 1998 and has its roots in older companies such as Alcatel and Nexans. In 2010 Intelecom merged with Carrot Communications and was acquired by Herkules Capital. The main office is located in Oslo, with branch offices in many other Norwegian cities, as well as Sweden, Denmark, Bulgaria and the UK. 

#### Herkules Capital
Since 2010, Intelecom Group and its subsidiaries have been fully owned by [Herkules Capital](http://www.herkulescapital.no/), the leading Norwegian private equity firm which supports established companies located in the Nordic region with strong growth potential.

### Authors
- Sven Ståle Osa
- Andreas Häber
- Morten Trydal
- Gunnar Grenlee
- Kjetil Johannesen

> **Note:** These documents replace the PDF only documentation which final version was _2.3.0_.

