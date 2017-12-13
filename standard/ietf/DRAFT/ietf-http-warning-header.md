# HTTP Warning Header  
> Proposed modifications to the HTTP Warning Header 
[RFC 7234 §5.5](https://tools.ietf.org/html/rfc7234#section-5.5)  

## Contributors
* BenC at Covea
* David Berlind
* Martin Burns
* Nathan Herring

## Syntax  
```
Warning: 299 <warn-agent> "<api-warn-code>, <api-warn-text>, <api-warn-detail-uri>, <api-warn-date>" [<warn-date>]
```  

### Directives  

`<warn-agent>`  
  The name or pseudonym of the server or software adding the Warning header 
  (might be "-" when the agent is unknown).  

`<api-warn-code>`  
  A simple code that can be handled by the client. (See below)  

`<api-warn-text>`  
  A human-readable message in English which corresponds to api-warn-code.  

`<api-warn-detail-uri>`  
  A URI of Content-Type application/json containing machine-readable information
  that the client code can use to handle the warning, such as retry delay or a 
  help link.  

`<api-warn-date>`  
  ISO 8601 date relevant to the Warning header. Could be one of: Deprecation 
  date, Maintenance date, Outage date.  

### Example  
```
Warning: 299 - "300, Deprecation, https://yoursite.com/details/300.json, 2017-12-12T23:28:18.508Z"
```  

## Warning Categories  

| api-warn-code | description               |  
| ------------- | ------------------------- |  
| 3xx           | API deprecation notices.  |  
| 4xx           | API version availability. |  
| 5xx           | Service disruption.       |  

## Warning Codes  

| api-warn-code | api-warn-text           | description |  
| ------------- | ----------------------- | ----------- |  
| 300           | Deprecated              | API has been deprecated. |  
| 310           | Pending Deprecation     | API is nearing deprecation. |  
| 320           | Scheduled Deprecation   | API has been scheduled for deprecation. |  
| 400           | New Version Available   | A new version of the API is generally available; begin transitioning to the latest version. |  
| 500           | Maintenance             | API is undergoing maintenance. |  
| 510           | Scheduled Maintenance   | API is scheduled for maintenance. |  
| 520           | Unscheduled Maintenance | API is undergoing an unscheduled maintenance. |  
| 530           | Service Degradation     | API is experiencing degraded performance. |  
| 540           | Outage - Partial        | API is experiencing a partial outage. |  
| 550           | Outage - Zonal          | API is experiencing an outage localized to an availability zone. |  
| 560           | Outage - Regional       | API is experiencing an outage localized to an availability region. |  
| 570           | Outage - Global         | API is experiencing an outage globally. |  

