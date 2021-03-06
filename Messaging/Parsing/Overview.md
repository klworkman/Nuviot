---
title: Parsing Overview
keywords: parsers, messaging, messages

created: 20170927
updated: 20170927
createdby: Kevin D. Wolf
updatedby: Kevin D. Wolf
---
[Home](Index.md) > [Device Messaging](../Index.md)

# Parsing Overview

Since in many cases you can't dictate what messages your devices will send, you can create contracts that define how data should be extracted from your messages.  Extracting this data is independent of the message source.  

In addition the same parsing system is used to extract Message Id's and Device Id's from the message.

### Message Components (Search Location)

Depending on the source of your message you will have different areas to extact fields from your mesage, in addition you will have meta data about the message (if applicable based on the listener you are using)

#### Headers
For HTTP sources such as REST or SOAP these are the [HTTP Headers](ParsingFromHeader.md) that come along with the message.  For other transport types additional data may be available.  See docuemtnation about the particular listener you are using.

#### Query String
This is primarily used for REST based protocols but can be used to extract values from a [query string](ParsingFromQueryString.md) using key value pairs

#### Topics
For pub/sub protocols, messages can be identified by [topics](ParsingFromTopic.md).

#### Path
In addition to the server and port number being available in your message if your message also specifies a resource address such as https://mydomain.coom/device/run/2342 the /device/run/2342 can be used to populate the message content.

#### Body or Payload

If you have a REST message this will be the POST or PUT content, most transports have some mechanism for passing data along with your message.  They body can be either [Binary](ParsingBinaryMessages.md) or Text, a Text message can be one of the following
* [String](ParsingStringMessage.md)
* [Delimited](ParsingDelimitedMessage.md)
* [JSON](ParsingJsonMessage.md)
* [XML](ParsingXMLMessage.md)

### Message Id and Device Id Parsers
An important part of processing the incoming data is to identify the [message id](MessageIdParsing.md) and [device id](DeviceIdParsing.md).
This can be extracted using the same mechanisms available to extract values for a message.
The difference is since we don't define the type of message, we need to include things such as delimiter, 
endiness and other values that are normally specified at the message level to extract the field.  

You can also use reg ex validation to ensure the field is in the correct format.

Your Message and Device Ids are always saved as strings.

### Message Value Parsers
There are two parts of defining how values are parsed out of a message, defining common paraemters such as the delimiter, quoted text, endiness at the message level.  Then for each field paticulars such as the field index or parameter name.  More details are available based on the type message.

There are three important parts of defining how your messages are parsed and used. 
* [Key](../../Topics/Keys.md) - The key will be used to identify this value as it's used to further process the message
* [Search Location](#Search-Location) - The Listener will populate different components that can be used to search for message values
* [Storage Type](#Storage-Types) - The data type that is used to identify the data


#### Search Locations
The following are four different areas that can be searched, these values are populated from the listener and more details are available there, in addition not all listeners support all the different locations.
* Headers
* Query String
* Path
* Body or Payload

#### Storage Types
These make up the type system that is used throughout the rest of the system
* String - Text, currently single byte ASCII text is supported
* Integer - 64 Bit Signed Integer
* Decimal - Double Precision Floating Point Number
* True False - Boolean
* GeoLocation - Stored as Latitude and Longitude in Decimal Degrees with 6 decimal points
* Date Time - Date Time Stored in [ISO 8601 Format](https://en.wikipedia.org/wiki/ISO_8601)

*Note* - Currently Arrays are not supported, please [contact us]('https://www.IoTAppStudio.com/Support/Request') if required for implementation

### Fine Tuning Selections
For any textual values you can use a [regular expression](RegExValueSelector.md) to extract a value. 

### Validating Message Values
Once a value is extracted you can use three mechanisms to [validate](Validation.md) the value prior to using it in yoru workflow





