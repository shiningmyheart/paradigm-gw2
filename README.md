<h1 align="center">Paradigm VM </h1>
<h4 align="center">Version 0.1 </h4>

[![GoDoc](https://godoc.org/github.com/paradigm-network/paradigm-vm?status.svg)](https://godoc.org/github.com/paradigm-network/paradigm-vm)
[![Go Report Card](https://goreportcard.com/badge/github.com/paradigm-network/paradigm-vm)](https://goreportcard.com/report/github.com/paradigm-network/paradigm-vm)
[![Travis](https://travis-ci.org/paradigm/paradigm.svg?branch=master)](https://travis-ci.org/paradigm/paradigm)
[![Discord](https://img.shields.io/discord/102860784329052160.svg)](https://discord.gg/kU3ewZQ)

Welcome to Paradigm Network !

The code is currently alpha quality, but is in the process of rapid development. The master code may be unstable; stable versions can be downloaded in the release page.


## Paradigm GW2 

Paradigm employs DAG-based structure to estabilish the FAAS architecture. In combination with the FAAS structure, there are two similarities between FAAS and DAG. 

>(1) **Scalability**: DAG is of good scalability and unlimited node growth. In FAAS, one function does only one thing, and can expands the volume independently without worrying about affecting other functions. And it can expands faster because of its smaller granularity. 

>(2) **Event driven**: In FAAS, functions does not publish any services, and does not consume any resources when no request is proposed.  Resources will be consumed to respond only when there is a request, and release immediately after the service. Due to this, FAAS naturally applies to any event-driven business scenario, such as  advertisement bidding, identity verification, timed tasks, and the emerging IoT applications. Messages are also transmitted by events in DAG network, which can be used as the event propagation channel of FAAS.


Function computing is naturally an event driven service. The core components of the function computing is the Function Execution Engine (FEE). FEE can be event-driven, that is, when an event occurs, the event triggers the execution of the function. Here, function computing supports API gateway as an event source. When the request setup function calculates the API for the back-end service, the API gateway triggers the corresponding function, which returns the execution result to the API gateway. It can be shown as follow. 


![images](https://github.com/shiningmyheart/paradigm-gw2/blob/master/images/pic-gw.png)


API gateway connects to the Function Execution Engine, you can safely open your functions in the form of API, and realize the functions of authentication, flow control, data conversion and other issues.


When an API gateway calls a function computing service, it converts the relevant data of the API into a Map format and passes it to the function computing service. After the function calculates the service, it returns the related data, such as statusCode, headers, body, in the form of Output Format. The API gateway then maps the content returned by the function calculation to the statusCode, header, body, etc. and returns it to the client.


## Parameter Format

The parameters are transmitted in the following fomat from the API gateway to the FEE. When the FEE is used as the back-end service of the API gateway, the API gateway transmits the request parameters to the input of the event computed by the FFE through a fixed Map structure. FEE obtains the required parameters through the following structure, and then processes.

	{
   	 "path":"api request path",
   	 "httpMethod":"request method name",
   	 "headers":{all headers,including system headers},
   	 "queryParameters":{query parameters},
   	 "pathParameters":{path parameters},
   	 "body":"string of request payload",
 	   "isBase64Encoded":"true|false, indicate if the body is Base64-encode"
	}



After the calculation of the FEE, it returns the parameter in the following JSON format. FEE returns the output to API gateway for furthering execution.

	{
    	 "isBase64Encoded":true|false,
	 "statusCode":httpStatusCode,
         "headers":{response headers},
         "body":"..."
	}
	
	
## Build development environment
The requirements to build Paradigm VM are:

- Golang version 1.9 or later
- Glide (a third party package management tool)
- Properly configured Go language environment
- Golang supported operating system	
	
