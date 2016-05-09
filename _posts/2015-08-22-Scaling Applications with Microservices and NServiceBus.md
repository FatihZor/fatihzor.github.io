---
layout: post
title:  "Scaling Applications with Microservices and NServiceBus"
date:   2015-11-18 06:22:15
categories:  [Scaling Applications with Microservices and NServiceBus]
tags:  [Microservice]
---

##Microservices

Micoroservices is a software architecture style,in which complex applications are composed of small, autonomous processs communicating with each other using language-agnostic APIs.

## Properites of Microservices

* Maintainable
* Versioning
* Each their own
* Hosting
* Failure isolation
* Observable

* UI
* Discovery
* Security
* Deployment

## NServiceBus


* An implementation of a service bus.
* Written for .NET services.
* Non- .NET services can use other bus implementatations compatible with the same messaging system.

## ESB

* Example:Biztalk
* Don't confuse with our service bus
* Logic in bus
* Micorservices = dumb pipes


* Monoliths are great but become unmaintainable when they get more complex* SOA with RPC and REST has some distinctive downsides* Microservices solve these downsides but beware of the complexity* The service bus facilitates the communication between services through a messaging backend



￼