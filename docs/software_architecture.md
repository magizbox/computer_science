# Service-Oriented Architecture

A service-oriented architecture (SOA) is an architectural pattern in computer software design in which application components provide services to other components via a communications protocol, typically over a network. The principles of service-orientation are independent of any vendor, product or technology. [^2]

![](http://www.logimethods.com/images/diagram-soa.gif)

## Generally accepted view [^1]

* Boundaries are explicit
* Services are autonomous
* Services share schema and contract, not class
* Service compatibility is based on policy

[^1]: [stackoverflow, Difference between Microservices Architecture and SOA](http://stackoverflow.com/questions/25501098/difference-between-microservices-architecture-and-soa)
[^2]: [wikipedia, Service-oriented architecture](https://en.wikipedia.org/wiki/Service-oriented_architecture)

# Microservices

> In computing, microservices is a software architecture style in which complex applications are composed of small, independent processes communicating with each other using language-agnostic APIs. These services are small building blocks, highly decoupled and focussed on doing a small task, facilitating a modular approach to system-building. One of concepts which integrates microservices as a software architecture style is dew computing. [^1]

![](http://image.slidesharecdn.com/microservicescfsummit-140611115438-phpapp01/95/cloud-foundry-and-microservices-a-mutualistic-symbiotic-relationship-17-638.jpg?cb=1402487864)

## Properties [^2]

* Each running in its own process
* Communicating with lightweight mechanisms, often an **HTTP resource API**
* Build around **business capabilities**
* **Independently deployable**
  * **fully automated** deployment
* Maybe in a **different programming language** and use **different data storage** technologies

## Monolith vs Microservice

<table>
<tr>
<th>Monolith</th>
<th>Microservice</th>
</tr>
<tr>
<td>Simplicity</td>
<td>Partial Deployment</td>
</tr>
<tr>
<td>Consistency</td>
<td>Availability</td>
</tr>
<tr>
<td>Inter-module refactoring</td>
<td>Preserve Modularity</td>
</tr>
<tr>
<td></td>
<td>Multiple Platforms</td>
</tr>
</table>

## Benefits [^4]

* Their small size enables developers to be most productive.
* It's easy to comprehend and test each service.
* You can correctly handle failure of any dependent service.
* They reduce impact of correlated failures.

[^1]: [Microservices](https://en.wikipedia.org/wiki/Microservices)
[^2]: [Slide 11/42, Micro-servies](http://www.slideshare.net/whyme/scalapeno-2014)
[^3]: [Martin Fowler, Microservices, youtube](https://youtu.be/wgdBVIX9ifA)
[^4]: [Rick E. Osowski, Microservices in action, Part 1: Introduction to microservices, IBM developerworks](http://www.ibm.com/developerworks/cloud/library/cl-bluemix-microservices-in-action-part-1-trs/)

# Web Service

# RESTful API

![](http://maxoffsky.com/word/wp-content/uploads/2012/11/RESTful-API-design-1014x457.jpg)

### REST Client

[Sense (Beta)](https://chrome.google.com/webstore/detail/sense-beta/lhjgkmllcaadmopgmanpapmpjgmfcfig?hl=en)

A JSON aware developer console to ElasticSearch.

### API Document and Client Generator

http://swagger.io/swagger-editor/


### API Client

**CRUD Pet**

<table>
<tbody>
<tr>
<td style="text-align: center;" colspan="4"><strong>API&nbsp;</strong></td>
<td style="text-align: center;"><strong>&nbsp;Client</strong></td>
</tr>
<tr>
<td style="text-align: center;"><strong>Method</strong></td>
<td style="text-align: center;"><strong>URL</strong></td>
<td style="text-align: center;"><strong>Body</strong></td>
<td style="text-align: center;"><strong>Return Body</strong></td>
<td style="text-align: center;"><strong>Method</strong></td>
</tr>
<tr>
<td>&nbsp;GET</td>
<td>/pets</td>
<td>&nbsp;</td>
<td>[Pet]</td>
<td>PetApi.list()</td>
</tr>
<tr>
<td>&nbsp;POST</td>
<td>/pets/</td>
<td>Pet</td>
<td>Pet</td>
<td>PetApi.create(pet)</td>
</tr>
<tr>
<td>&nbsp;GET</td>
<td>/pets/pet_id</td>
<td>&nbsp;</td>
<td>Pet</td>
<td>PetApi.get(pet_id)</td>
</tr>
<tr>
<td>&nbsp;PUT</td>
<td>&nbsp;/pets/pet_id</td>
<td>Pet</td>
<td>Pet</td>
<td>PetApi.update(pet_id, pet)</td>
</tr>
<tr>
<td>&nbsp;DELETE</td>
<td>/pets/pet_id</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>PetApi.delete(pet_id)</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>

**CRUD Store**

<table>
<tbody>
<tr>
<td>GET /stores</td>
<td>StoreApi.list()</td>
</tr>
<tr>
<td>...</td>
<td>...</td>
</tr>
</tbody>
</table>

**Relationships**

Many to many

<table>
<tbody>
<tr>
<td>GET /stores/sotre_id/pets</td>
<td>StoreApi.get_pets(store_id)</td>
</tr>
</tbody>

### Example

[https://api.facebook.com/method/links.getStats?urls=%%URL%%&format=json](https://api.facebook.com/method/links.getStats?urls=%%URL%%&format=json)