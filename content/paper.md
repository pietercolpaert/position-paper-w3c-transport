## Linked Data Ontologies
{:#ld-ontologies}

Mobility as a Service means ecosystem building: every organization fulfills a small piece of the mobility puzzle. Standards are useful, but not one standard is going to be able to describe the entire world. Moreover, even for describing similar things, multiple standards exist. MaaS crosses the borders of organizations, but also crosses the borders of domains standards are built for.

Linked Data proposes a framework to help raise the interoperability of different standards and datasets. It advocates two things: 1) supporting multiple serializations through the Resource Description Framwork, and 2) using HTTP URIs for identifiers.

The [Resource Description Framework](https://www.w3.org/TR/rdf11-primer/) specifies a triple structure for statements in datasets. A subject has a relation (a predicate) to something else (the object). A dataset is then a list of statements or triples. Such triples can be extracted from any kind of serialization such as CSV, JSON or XML, however, we need a standard to know how these triples are encoded in the file. This is the small layer that RDF1.1 adds to e.g., JSON (with [JSON-LD](https://www.w3.org/2018/jsonld-cg-reports/json-ld/)), XML (with [RDF/XML](https://www.w3.org/TR/rdf-syntax-grammar/)) or CSV (with [CSV on the Web](https://www.w3.org/TR/tabular-data-primer/)).

For each part of such a triple, an identifier should be used. E.g., 1 has a first name “Pieter”. However, 1 can mean a lot of things in a decentralized context. Thus, Linked Data advocates for a web address to be used. My personal identifier is <https://pietercolpaert.be/#me>, yet others have also given me the URIs <https://orcid.org/0000-0001-6917-2167> and <https://dblp.org/pers/c/Colpaert:Pieter>. It is up to me to decide what I want to use in my own context, but can easily make my data interoperable with other contexts by declaring these links.

Linked Data does not solve semantic interoperability for these standards and datasets. However, it does create a machine interpretable framework to discuss the semantics. In this way, when using a term, you can be certain that it is the intended term from within a specific standard. It also opens the door towards automated alignments between standards, although it is still early days. Existing domain models and standards can be used within Linked Data with a relatively small effort. All terms defined in the domain model need an HTTP URI that when resolved, will return a definition of that term. Our pitch for creating a Linked Data specification of the CEN Transmodel standard can be found at https://speakerdeck.com/pietercolpaert/transmodel-as-linked-data-the-first-step

## Cost-efficient Web APIs for serverless clients
{:#web-apis}

A false dichotomy when publishing transport data must be when people choose between downloading the data dump or using an existing route planning API. 
A data dump gives all flexibility to calculate any kind of specific route useful for the modes you want to support.
However, it requires you yourself to do heavy data lifting on your own servers: you will need a road network, integrate public transport datasets worldwide, add specific weight to the routing graph, set up route planning software and so forth.
Using an existing route planner however makes you dependent on the use cases and datasets the route planner supports.
If it does not support taking your foldable bike on public transport, you are not in luck and your only options remains doing the heavy data lifting yourself.

In-between solutions taking the best from both worlds (serverless route planners while keeping any kind of flexibility to the client) exist.
When the dataset is [fragmented](http://linkeddatafragments.org) in well-chosen documents, a route planner can download only the parts of the dataset it needs just in time.
We have already developed two hypermedia APIs: one for [public transport services using Linked Connections](http://linkedconnections.org), and another for republishing the [road network of OpenStreetMap](http://pieter.pm/demo-paper-routable-tiles/). Using this idea of fragmenting datasets in the right parts, developers can code their applications entirely serverless if they want to, and data owners still have a cheap web interface to host that will not overload their servers on increasing demand thanks to the high cacheability and ease to host.
Having started our own route planner implementation in JavaScript at https://planner.js.org, we are now looking at others to create other hypermedia interfaces we could start reusing for our serverless route planning library.

## Protocols for decentralized mobility profiles
{:#my-data}

The [W3C SOLID community group](https://www.w3.org/community/solid/) proposes W3C standards for the read-write Web to decentralize personal information for Web applications.
In essence, everyone should be able to decide where their data is stored, and which services get access to the data.
Also for Mobility as a Service, the Flemish mobility company De Lijn and our team at Ghent University started to collaborate on mobility profiles.
These profiles are owned by the end-user, but the Flemish mobility company can write interesting data to it.
For example: which subscription they own, their preferred routes, whether or not they own a car-sharing subscription, a foldable bike, etc.
When using a different route planner, this end-user should be able to decide to give the route planner access to this mobility profile to calculate individual route planning advice.

We are only at the advent of the idea of decentralized mobility profiles, yet everyone can play a role by putting the data itself where it belongs: in the control of the end-user.
We will create a better and stronger Mobility as a Service ecosystem when all route planners have equal access to both open transport data and the individual mobility profiles of users (if they give their consent).
