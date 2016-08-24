# PoGo-Proxy.NET

This project is a .net MITM proxy designed to read all the API messages sent between the Pokemon Go device and the Pokemon Go servers. By reading this data, you can make informed decisions about which Pokemon to keep, and so on.

The [POGOProtocs](https://github.com/AeonLucid/POGOProtos) repo is used as a source for protoc files.

# Usage

## Setting Up

In order to get this up a running, you have to run through a couple of steps:

* First modify the Ip settings in the ProxyController.cs file
  * Find your local ip address and set that as the string ip for the following line:       
  * var explicitEndPoint = new ExplicitProxyEndPoint(IPAddress.Parse(ip), Port, true);
  * where ip should be something like 
  *var explicitEndPoint = new ExplicitProxyEndPoint(IPAddress.Parse("192.168.0.10"), Port, true);
  * Keep the port as is or update the port to whatever you want
* Then, run the project once to generate the CA certificate. This will add the certificate to your computer. You also need to export this certificate and add it to your android device.
* Once you have the certifcates in place, set your Pokemon Go device to use the proxy config
  * You need to connect to the same network the host device is connected to
  * Go into the network settings and set the Ip address and host with the values from earlier 

## Getting started

Once you have everything set up, just start up the sample project on your host device, then open the Pokemon Go app on your phone/tablet. You should start to see the api requests and responses populate the console window. These aren't very readable at the moment, but you can take a look at the generated log file when you end the proxy.

## Certificate Pinning

As of version 0.31, Niantic added certificate pinning to Pokemon Go. In order to use this MITM proxy, you have to do a little extra work. You can either modify the apk to accept other certificates [as shown here](https://eaton-works.com/2016/07/31/reverse-engineering-and-removing-pokemon-gos-certificate-pinning/), or you can use something like XPosed to get around the certificate pinning on the fly.

# Dependencies

This project is built in Visual Studio 2015 with the following nuget packages:
* DotNetZip v1.9.8
* Google.Protobuf v3.0.0-beta4
* Newtonsoft.Json v9.0.1
* Titanium.Web.Proxy v2.3000.185

Python 2.7 is also required to decode the [POGOProtocs]() and run the pre-build event that adds them to the project.
