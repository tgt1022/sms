# REST API

[Back to main page](https://github.com/Intelecom/sms/) - [Table of contents](/sections/overview.md) - [Previous section](/sections/interfaces-general.md) -  [Next section](/sections/interfaces/soap.md)

This section describes how to integrate towards the Intelecom SMS Gateway REST API. The Rest API supports both sending SMS (MT), receiving SMS (MO) and delivery reports (DR). Please see [here](/sections/common.md) for information about the available message parameters.

## Sending messages (MT)

### How to connect

The REST MT interface for sending SMS supports XML, JSON and web forms over HTTP POST on the following URL:


	https://<server-url>/gw/rs/sendMessages 

### Regarding content types

To specify the content type of the request, you must specify the “Content-Type” header and to specify the content type of the response you must specify the “Accept” header. Valid values are:

* JSON:  “application/json”
* XML: “application/xml”
* Web forms: “application/x-www-form-urlencoded”

Note that web forms do not have a special response format so it will use XML (default) or JSON based on the Accept-header.

### Encoding

The content encoding should be UTF-8

### XML Schema definition

The XML request and response uses the same schema used in the WSDL definition for the SOAP interface:

	https://<server-url>/gw/SMSGateway?wsdl

### XML Request Example

	<?xml version="1.0"?>
	<req:request xmlns:req=http://chimera.intele.com/gw/xsd/SMSGateway/Request/2013/02 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
		<serviceId>1000</serviceId>
		<username>intelecom</username>
		<password>xdyf3bf2</password>
		<message>
			<recipient>+4741000000</recipient>
			<content>This is a message from Intelecom.</content>
			<price>0</price>
			<settings>
				<originatorSettings>
					<originator>Intelecom</originator>
					<originatorType>Alphanumeric</originatorType>
				</originatorSettings>
				<safeRemoveNonGsmCharacters>true</safeRemoveNonGsmCharacters>
			</settings>
		</message>
	</req:request>

### XML Response Example

	<?xml version="1.0" standalone="yes"?>
	<ns2:response xmlns:ns2="http://chimera.intele.com/gw/xsd/SMSGateway/Response/2013/02">
		<messageStatus>
			<statusCode>1</statusCode>
			<statusMessage>Message enqueued for sending</statusMessage>
			<recipient>+4741000000</recipient>
			<messageId>760081j04w00</messageId>
			<sequenceIndex>1</sequenceIndex>
		</messageStatus>
	</ns2:response>

### JSON Request Example

	{
	    "serviceId":1000,
	    "username":"intelecom",
	    "password":"xdyf3bf2",
	    "message":[
	        {
	            "recipient":"+4741000000",
	            "content":"This is a message from Intelecom.",
	            "price":0,
	            "settings":{
	                "originatorSettings":{
	                    "originator":"Intelecom",
	                    "originatorType":"ALPHANUMERIC"
	                },
	            }
	        }
	    ]
	}

### JSON Response Example

	{
	    "messageStatus":[
	        {
	            "statusCode":1,
	            "statusMessage":"Message enqueued for sending",
	            "clientReference":null,
	            "recipient":"+4741000000",
	            "messageId":"760081j1ll00",
	            "sessionId":null,
	            "sequenceIndex":1
	        }
	    ]
	}

### Web Request Example

	POST /gw/rs/sendMessages HTTP/1.1
	Host: smsgw.intele.com
	Cache-Control: no-cache
	Content-Type: application/x-www-form-urlencoded
	
	serviceId=1000&username=intelecom&password=xdyf3bf2&message%5B0%5D.recipient=%2B4710000000&message%5B0%5D.content=Test+is+a+message+from+Intelecom



## Receiving messages (MO)

If you want to enable end users to send SMS messages to your solution via REST you will need to set up a service able of receiving HTTP POST requests through a REST API with either JSON or XML formatting. The REST API will accumulate batches of messages and only send 1 request per second. This means that you can expect that you sometimes will get XML or JSON messages that contain more than one message / delivery report.

The SMSGW will invoke your HTTP service when MO messages are slated for delivery to your server. The URL of your service must be provided to Intelecom Interactive Service Desk ([support.interactive@intele.com](mailto:support.interactive@intele.com)) for proper configuration of the service. You also need to provide information of which content-type you want to use (HTTP POST with JSON or HTTP POST with XML).

If you need to add a firewall rule, all requests will originate from IP: 212.89.48.14.

[ngrok](/references/ngrok.md) is a great tool to use when testing MO / DR messages locally. 

For description of incoming SMS (MO) parameters see [this section](/sections/common.md#parameters-for-incoming-mo-messages).

### HTTP POST example with JSON formatted data

	{
	   "mo":[
	      {
	         "messageid":"7a02c0000f00",
	         "serviceid":123,
	         "servicename":"Testtjeneste",
	         "sno":"1960",
	         "originator":"+4799999999",
	         "mcc":242,
	         "mnc":1,
	         "content":"Kodeord Testmelding 1",
	         "command":"Kodeord",
	         "strippedcontent":"Testmelding 1",
	         "type":1,
	         "timestamp":"20140206 11:45:33",
	         "sctimestamp":"20140206 11:45:33",
	         "sessionid":"1234567890"
	      },
	      {
	         "messageid":"7a02c0000g00",
	         "serviceid":123,
	         "servicename":"Testtjeneste",
	         "sno":"1960",
	         "originator":"+4744444444",
	         "mcc":242,
	         "mnc":1,
	         "content":"Kodeord Testmelding 2",
	         "command":"Kodeord",
	         "strippedcontent":"Testmelding 2",
	         "type":1,
	         "timestamp":"20140206 11:47:33",
	         "sctimestamp":"20140206 11:47:33",
	         "sessionid":"1234567890"
	      }
	   ]
	}


### HTTP POST example with XML formatted data

	<?xml version="1.0" encoding="UTF-8"?>
	<mo>
		<message>
			<messageid>7a02c0000f00</messageid>
			<serviceid>123</serviceid>
			<servicename>Testtjeneste</servicename>
			<sno>1960</sno>		
			<originator>+4799999999</originator>
			<mcc>242</mcc>
			<mnc>1</mnc>
			<content>Kodeord Testmelding 1</content>
			<command>Kodeord</command>
			<strippedcontent>Testmelding 1</strippedcontent>		
			<type>1</type>		
			<timestamp>20140206 12:41:13</timestamp>		
			<sctimestamp>20140206 12:41:13</sctimestamp>		
			<sessionid/>		
		</message>
		<message>
			<messageid>7a02c0000g00</messageid>
			<serviceid>123</serviceid>
			<servicename>Testtjeneste</servicename>
			<sno>1960</sno>		
			<originator>+4744444444</originator>
			<mcc>242</mcc>
			<mnc>1</mnc>
			<content>Kodeord Testmelding 2</content>
			<command>Kodeord</command>
			<strippedcontent>Testmelding 2</strippedcontent>		
			<type>1</type>		
			<timestamp>20140206 12:43:15</timestamp>		
			<sctimestamp>20140206 12:43:15</sctimestamp>		
			<sessionid/>
		</message>
	</mo>

## Receiving Delivery Report (DR) messages

If you need to know whether a specific message is received by the end users handset or not, you will need to implement a server side service able of receiving HTTP POST requests through a REST API with either JSON or XML formatted content. 

This is an asynchronous operation and you will need to implement a mechanism for storing messageid and/ or batchReference and/ or clientReference from sent (MT) messages in order to associate an incoming delivery report (DR) to the correct MT message.

[ngrok](/references/ngrok.md) is a great tool to use when testing MO / DR messages locally. 

For description of delivery report parameters see [this section](/sections/common.md#parameters-for-delivery-reports-dr).

### HTTP POST example with JSON formatted data
	
	{"dr":[
			{
			"messageid":"6y034000cy00",
			"customerbatchreference":"MyBatch001",
			"customermessagereference":"MyRef123",
			"serviceid":123,
			"servicename":"Testtjeneste",
			"mcc":242,
			"mnc":1,
			"type":6,
			"statuscode":0,
			"statusdescription":"OK. Message processed successfully.",
			"extstatuscode":"0",
			"extstatusdescription":"Delivered"
			},
			{
			"messageid":"6y034000dy00",
			"customerbatchreference":"MyBatch001",
			"customermessagereference":"MyRef124",
			"serviceid":123,
			"servicename":"Testtjeneste",
			"mcc":242,
			"mnc":1,
			"type":6,
			"statuscode":0,
			"statusdescription":"OK. Message processed successfully.",
			"extstatuscode":"0",
			"extstatusdescription":"Delivered"
			}
	]}

### HTTP POST example with XML formatted data

	<?xml version="1.0" encoding="UTF-8"?>
	<dr>
		<message>
			<messageid>6y034000cy00</messageid>
			<customerbatchreference>MyBatch001</customerbatchreference>
			<customermessagereference>MyRef123</customermessagereference>
			<serviceid>123</serviceid>		
			<servicename>Testtjeneste</servicename>
			<mcc>242</mcc>
			<mnc>1</mnc>		
			<type>6</type>		
			<statuscode>0</statuscode>
			<statusdescription>OK. Message processed successfully.</statusdescription>
			<extstatuscode>0</extstatuscode>
			<extstatusdescription>Delivered</extstatusdescription>
		</message>
		<message>
			<messageid>6y034000dy00</messageid>
			<customerbatchreference>MyBatch001</customerbatchreference>
			<customermessagereference>MyRef124</customermessagereference>
			<serviceid>123</serviceid>		
			<servicename>Testtjeneste</servicename>
			<mcc>242</mcc>
			<mnc>1</mnc>		
			<type>6</type>		
			<statuscode>0</statuscode>
			<statusdescription>OK. Message processed successfully.</statusdescription>
			<extstatuscode>0</extstatuscode>
			<extstatusdescription>Delivered</extstatusdescription>
		</message>
	</dr>

## HTTP response for incoming SMS (MO) and Delivery Report (DR) messages

Your server must respond to the HTTP request with a HTTP 200 header response, any other response code will by default cause a retry of delivery.

If the gateway does not receive a HTTP 200 acknowledge it will try resending the message to the CP. The MessageId will be the same as the previous attempt. Normally the MO-request will wait 60 seconds for the HTTP 200 response. If your server does not respond within the time limit, the message is marked as undelivered and the gateway will try to resend the message later. 

**IMPORTANT:** Respond as fast as possible on the request before you start doing heavy business logic. It is strongly recommended to use an asynchronous model where you acknowledge the message and add it to an internal queue, for example database. Do not use a synchronous model where you do all the business logic and then send a response message. Our experience is that customers that fail to respond within the time limit of the request often experience that their messages are queued. This is because the system will use some of its resources to resubmit messages that your server has received earlier but failed to acknowledge. The higher the traffic peaks, the more significant this problem will be.

