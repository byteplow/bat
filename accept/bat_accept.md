---
tags: bat, activitypub
---
# bat accept

## state
+ 2020.12.15 started this document

## rules

| regex | description
|-|-
| `§.*` | a definde key word
| `%.*` | a keyword that moust be replaced with the proper term
| `$.*` | short cut
| `~.*` | find a better / more specifc word

## short cuts

| short cut | long form
|-|-
| did | an distributed identifire == verteilte ID not Verteilte ID (it is not the same as §did this refrest to the standart did)

## theses v1
extanding activity pub with distributed identeties
+ an §actor must be identified by an $did
+ an the $did must be universally uniqued
+ an $did must not contain any server spectifc information
    + like not user@server.com or https://server.com/u/users
    + but it would be technikal ok if the server specific information is only needed during id creation. And the id can then be used with any server.
        + then we need to consider that an §actor might not want to be connected with this any server any more....
+ it must be possible for an §actor to send %activities to and §actor by its $did
+ it must be easy and fast to look up an $did
    + a metric for this is needed
    + there should is no significant delay after the first lookup
    + the fist look up should not take TIME wenn done on the server (async)
    + the fist look up should not take TIME wenn done on the client (sync)
        + solution: if it takes longer sync lookup must not be used
+ activity pub servers that dont support our extension should still be able to communicate with us
    + there are multible steps for this:
        + server can just kommunikate with the standart protocol
        + server preservse information so that if it is updated it can uses this information
        + server preservse information so that a client supporting our extension can use it
        + server preservse the information so that another server/client can use this information
            + eg. if our %message is %retreted/commented by an client at an unsupporting server and server readding ths new %message can use the did infor mation of the original %message
+ activity pub clintes no understanding our extension still can communite with us
    + with our server as client
    + or as client form an unsupporting server
    + there are also more steps:
        + no $did preservation
        + $did preservation for future use, if updated
        + $did redistriputen. so that supporing clitens can used still use it
+ the implementation should be standart conform ^^
+ the implementation slould be compadible with other extension
    + jsonld
    + should not modife original fileds, also if all $particcipants (servers and clients) suppored the extension

## problem v1
+ identaty is bound to a server
    + server gose down, temporary or permanent
    + server policy changes
+ its hard to change the server
+ u need to follow the &actors u follows again
+ u lose ur followers / the followers lose u
+ now one cat determit if ur new identety is realy u.
    + u could post with ur old id, but no if the servers are down
+ there most &actors in eg. &mastodon are on a few big server
    + this is agains decentrelastation
    + this could allow them to change to a differnt server
## theses v2
A server change should have following properteis:
+ &actors which have seen u before, can determen ur the same &actor
+ u dont lose ur flllowers (lose mening u still know them and messages for the %u:following groub are deliverd correctly)
+ u dont lose the people u are following (lose mening u still know them and messages for the %u:following groub are deliverd correctly)
+ messages %refering to old %actifiteys (before the change), will be delivert correktly
+ %public messages wont be lost
This problems could be sloved with an $did.
The $did would need to have following properties:
+ an §actor must be identified by an $did
+ an the $did must be universally uniqued
+ an $did must not contain any server spectifc information
    + like not user@server.com or https://server.com/u/users
    + but it would be technikal ok if the server specific information is only needed during id creation. And the id can then be used with any server.
        + then we need to consider that an §actor might not want to be connected with this any server any more....
+ it must be possible for an §actor to send %activities to and §actor by its $did
+ it must be easy and fast to look up an $did
    + a metric for this is needed
    + there should is no significant delay after the first lookup
    + the fist look up should not take TIME wenn done on the server (async)
    + the fist look up should not take TIME wenn done on the client (sync)
        + solution: if it takes longer sync lookup must not be used
Our protocol should have following properties:
+ activity pub servers that dont support our extension should still be able to communicate with us
    + there are multible steps for this:
        + server can just kommunikate with the standart protocol
        + server preservse information so that if it is updated it can uses this information
        + server preservse information so that a client supporting our extension can use it
        + server preservse the information so that another server/client can use this information
            + eg. if our %message is %retreted/commented by an client at an unsupporting server and server readding ths new %message can use the did infor mation of the original %message
+ activity pub clintes no understanding our extension still can communite with us
    + with our server as client
    + or as client form an unsupporting server
    + there are also more steps:
        + no $did preservation
        + $did preservation for future use, if updated
        + $did redistriputen. so that supporing clitens can used still use it
+ the implementation should be standart conform ^^
+ the implementation slould be compadible with other extension
    + jsonld
    + should not modife original fileds, also if all $particcipants (servers and clients) suppored the extension
## theses v3
A server change should have following properteis:
1. §Actor B has ~seen, §actor A before its server change. Then &actor B can determen, that an §actor from a differten server, is acctualy &actor A.
1. If §actor a changes the server, it would not lose its §followers collection. So §activities from §actor a to its §followers are deliverd correctly. Also §activities form §actor b to §actor a´s §followers are deliverd correctly.
1. If §actor b changes the server, if would not lose its $following collection. So §activities from &actor b, wiche &actor a follows, to its followers, will be deliverd correctly to §actro a. §Activities from another §actor c to §actro b´s followers, will be correctly delivert to §actor a.
1. §Activity y from §actor b should be send to §actor a, becouse it referse to an §activity x. §Activity x was ~created/deliverd before $actor a changed the server. §Activity y should be deliverd correctly to §actor a. §Actor a and b clould be the same &actor. 
1. If §actor a changes the server, public or groub accessable §activities, will stay publicly or groub accessable. Like public $activities in its outbox or liked §activities.
The protocol extension should be compatible with non supporting clients or servers:
1. Server a dose not support the extension. Server a can still communicate with clients and servers using the extension.
1. Server a dose not support the extension. Server a can preserve the extensions information. Server a can uses thes information, if it is update.
1. Server a dose not support the extension. Server a can preserve the extensions information. Client of server a, which supports the extension, can use the information.
1. Server a dose not support the extension. Server a can preserve the extensions information. So that a client from a diffrent server can use the information.
1. Client a dose not support the extension. Client a can still communicate with clients and servers using the extension.
1. Client a dose not support the extension. Client a can preserve the extensions information. Client a can uses thes information, if it is update.
1. Client a dose not support the extension. Client a can preserve the extensions information. Client of server a, which supports the extension, can use the information.
1. The protocol extension should not introduce significant latency. (yeah know that a metric is missing, but there should be a differtens times for clinet and server)
## theses v4
1. The protocol communication should not depend on dns. Did methodes might use dns.
1. The protocol communication should not depend on global certificate authoroties. Did methodes might use global certificate authoroties.
1. A server change should have following properteis:
    1. §Actor B has ~seen, §actor A before its server change. Then &actor B must be able to determen, that an §actor from a differten server, is acctualy &actor A.
    1. If §actor a changes the server, it must not lose its §followers collection. §Activities to §actor as $followers collection must be deliverd correctly. (So §activities from §actor a to its §followers are deliverd correctly. Also §activities form §actor b to §actor a´s §followers are deliverd correctly.)
    1. If §actor b changes the server, if must not lose its $following connections. So §activities from &actor b, which &actor a follows, to its followers, will be deliverd correctly to §actro a. §Activities from another §actor c to §actro b´s followers, will be correctly delivert to §actor a.
    1. §Activity y from §actor b should be send to §actor a, becouse it referse to an §activity x. §Activity x was ~created/deliverd before $actor a changed the server. §Activity y must be deliverd correctly to §actor a. §Actor a and b clould be the same &actor.
    1. If §actor a changes the server, public or groub accessable §activities, must stay publicly or groub accessable. Like public $activities in its outbox or liked §activities.

2. The protocol extension should be compatible with non supporting clients or servers:
    1. Server a dose not support the extension. Server a must be able to communicate with clients and servers using the extension.
    1. Server a dose not support the extension. Server a must be able to preserve the extensions information. Server a can uses thes information, if it is update.
    1. Server a dose not support the extension. Server a must be able to preserve the extensions information. Client of server a, which supports the extension, can use the information.
    1. Server a dose not support the extension. Client a must be able to the extensions information. So that a client from a diffrent server can use the information.
    1. Client a dose not support the extension. Client a must be able to communicate with clients and servers using the extension.
    1. Client a dose not support the extension. Client a must be able to preserve the extensions information. Client a can uses thes information, if it is update.
    1. Client a dose not support the extension. Client a must be able to preserve the extensions information. Client of server a, which supports the extension, can use the information.
    1. The protocol extension must not introduce significant latency. (yeah - know that a metric is missing, but there should be a differtens times for clinet and server)
## solutions
+ use did as an additional user id.
    + did document contains user page
        + private information should not be store in did documents
    + did gets resolved to %https uri users%
        + note: uri should not be %human redable%, no private information in did documents (see did spec ...)
        + Fulfills theses 1.1: did is not bound to the server and never changes
        + Fulfills theses 1.2: b´s followers collection contains a´s did
        + mostly Fulfills theses 1.4 as long as actor a is addrest by its did or by another actros collection
            + actor a´s collections cant be found any more (they are not addressed by its did), so if actor a is addressed by its own collection this wont work. Also not if the owne of the collection also changed the server.

+ use the id base on the did as an additonal id for all its objects
    + make d did server that resolves to dns or ip. extend https uris to suppored did as host
    + make a uri that can be resolved to a http uri with well known format
    + make a uri that can be resolved to a http uri with the help of an template, hosted at the actifity pub server and is linked form the did document
    + collections an object that need to be keeped need to be copyed on server change
    + use data shards to store objects / collections distributed or some other custom methode
        + fulfills theses 1.5
    + all fulfill theses 1.4

+ Store objects notes distributed
    + data shards
    + copy them wenn changing servers
    + all fulfill theses 1.5
## accept v1

### Introduction

ActivityPub is a decentralized socual networking protocol. ActivityPub is base on event publishing. There are tow clases of nodes server and clients. Server form a peer to peer network. They acct as mailboxes for there clients. Clients do not have to online all the time. They recive events by querring ther mailbox on a specific server perioticly. Clients also send events via there servers, to reduce therie network load. 

Multible decentralized social networks use ActivityPub. For example the microblogging platform Mastodon and PeerTube a video hosting platform. Mastodon has milions of users. But there are still many unsolved problems in the ActivityPub world. One of them is, that the actors (user) id is tight to there server. An user id is an uri (mostly https) to there actor object. Becouse of that an actor can not change its server, without loosing its identety.

There are multible resonse for an actor to want to change there server. Moderration is another unsolved problem in the ActivityPub EcoSystem. Many servers experiment with different aproches of moderrating. Mostly they use server black or white listing. An actor that dose not like there severs moderration policiy 
might want to change there server.
ActrivityPub server are mostly operrated by people in ther free time. ESpeacaly smaler instances can have probles finding an new operrater. If an instance gose down all users need to create a new identety on another instance and lose all there connections to other actors. This might also be a resone why moste people desice to join a big instance.

The majority of all mastodon users is on a few big instances. That is a bad for decentraliation. Giving actors the option to change there server, might help user to distributing user more evenly. If they do not have to fear to lose der identey on a smal instance. It would also provide users alreay using an big activtiypub instacne, to switche to a smaler one.

To provide the ability to change the server, ActivityPub needs an actor id which is not linked to a specific server. One solution would be an decentralised or distributed id. Decentralized Identifiers is an w3c standat (Working Draft), specifing souch an id.

Decentralized Identifiers specifs an did. An did consists of a methode and an methode specific id. The methode specifys the functionalaty. Methodes offten use distibuted ledgers as a key value store. And did can be resolved to an did document. The did document contains information to authernticate and verify the did subject. A did document can alos specify services. Services are methodes to communicate or interact with the did subject. This can be an uri pointing to a website or a mailto uri. But it also could be a uri pointion to an actrivtypub actor object.

### Objective

The objective is to extent ActivityPub with w3c did, to allows actors to changes servers, without losing there identety. The protocol should not rely on clients or servers having an domain name or and tls certificate singed by an global certfifcate authority. The protocol extension should be optional backwards compatible. Backwards compatability may use dns and global certificat authorities.

In the batchlor theses i will specify this extension and implement a protype referenc server and a prototype referenc client.
The prototype reference client has no ui, only an api.

#### Requierments

To fulfill the objective atleast these requirements need to be met:

1. A server change should have following properteis:
    1. §Actor B has ~seen, §actor A before its server change. Then &actor B must be able to determen, that an §actor from a differten server, is acctualy &actor A.
    1. If §actor a changes the server, it must not lose its §followers collection. §Activities to §actor as $followers collection must be deliverd correctly. (So §activities from §actor a to its §followers are deliverd correctly. Also §activities form §actor b to §actor a´s §followers are deliverd correctly.)
    1. If §actor b changes the server, if must not lose its $following connections. So §activities from &actor b, which &actor a follows, to its followers, will be deliverd correctly to §actro a. §Activities from another §actor c to §actro b´s followers, will be correctly delivert to §actor a.
    1. §Activity y from §actor b should be send to §actor a, becouse it referse to an §activity x. §Activity x was ~created/deliverd before $actor a changed the server. §Activity y must be deliverd correctly to §actor a. §Actor a and b clould be the same &actor.
    1. If §actor a changes the server, public or groub accessable §activities, must stay publicly or groub accessable. Like public $activities in its outbox or liked §activities.

1. The protocol extension should be compatible with non supporting clients or servers:
    1. Server a dose not support the extension. Server a must be able to communicate with clients and servers using the extension.
    1. Server a dose not support the extension. Server a must be able to preserve the extensions information. Server a can uses thes information, if it is update.
    1. Server a dose not support the extension. Server a must be able to preserve the extensions information. Client of server a, which supports the extension, can use the information.
    1. Server a dose not support the extension. Client a must be able to the extensions information. So that a client from a diffrent server can use the information.
    1. Client a dose not support the extension. Client a must be able to communicate with clients and servers using the extension.
    1. Client a dose not support the extension. Client a must be able to preserve the extensions information. Client a can uses thes information, if it is update.
    1. Client a dose not support the extension. Client a must be able to preserve the extensions information. Client of server a, which supports the extension, can use the information.
    1. The protocol extension must not introduce significant latency. (yeah - know that a metric is missing)

#### Tests

To validate if the protocol extension mets the requirements, the prototype referenc implementation is tested.

The test setup constists of multible servers and clients. For most test there is the actors original server, the server the actor changes to and an third 
uninvolved server. Every actor has its own client. The clients are controled by an API. 

Servers and Clients communicate over a local network. There communication is typacly encryped with https, but the test setup might use unencrypted http.
For testing a local did provider might be used.

The test cases are derived from the requirements. Each requiremets has atleast one test. Test for requiremets 1. are repeated multible times. Every time &actor b ues a differten server. Actor b is the actor that dose not changes the server. Actor a is the one that chages the server. Actor b uses the actors a´s origian server, the server actor a changes to and the 
uninvolved server.

Test for requiremets 1. are repeated, with actor a´s original server turned of after server change.

### Solution

A solution constis of three parts. The first one identifies an actor object using a did. The second one identifies collections by using an id based on the actors did. The tired part is the actula srver change.

#### first part
To uses a did as an actor id, it musst be possible to revolve a did to an actor object. This is archived by adding an serviceEndpoint to the did document. The ServiceEndpoint contains the actor objects uri.

The did actor id can be resolved to the actor object uri with standart did tooling. The actor object can then be retrived with an uri specific methored (e.g https).

#### second part
To be able to use collections after a server change. The collection id need to be tight to the users identity.
Therefore we need a custom uri, which is base on the did.
I have theer ideas how to solve this. 

##### methode 1 - json-ld path uri
Collections are identifiedy by a custom uri. The uri is based on the did. And resolves to the collections uri. (the collectins id if our extension, would not be ues)

An collections can be located at an arbitrarily uri. The uris structure and format can change form implementaition to implementation.
Therefore the uri can not be resoved by any mapping sceam.

The uris path is a json-ld path. It points to a location in the actor onject where the collection uri can be found.

This methode can only resolve collections, wiche are part of the actor object.

##### methode 2 - https with did
Collections can be represented by a custom uri. It is based on the did.

The custom uri basicly extends https. To allow a did as host in an https uri.

A servce endpoint in a did document, is used to resolve the did to an ip address.

This methode would require the all implementations to use the same uri scheam.

##### methode 3 - an activityPub object identifiyer
Collections can be represented by a custom uri. It is based on the did.

The uri consists of a did and an object id (string). 
A mapping from the custom uri to an specific https uri is possible. This is technicaly used to retived a Collection.
The resoleved https uri should not be used on its own.

This methode uses uris with no features. This dose not allow differtent implementations to use different uris. 
But other extension might need to extend this uri.

#### thierd part
To change the server all actor information need to be copyed and the did document must be updated.

A server change is carried out by the client. The client creates an actor object and all collection object it wants to keep on the new server.
The client may use objects form its local cache, if the original server is unavaliable. If successfull the client can update its did document, with the new actor object uri. Then the clien should delete its actor object on the original server.

If the new server needs registration, the client needs to register first. Authentication and registration is not part of this extension.









## Accept v2
### Introduction
ActivityPub is a decentralized social networking protocol. ActivityPub is base on event publishing. There are tow class of nodes server and clients. Server form a peer to peer network. They acct as mailboxes for there clients. Clients do not have to online all the time. They receive events by queering there mailbox on a specific server periodically. Clients also send events via there servers.
Multiple decentralized social networks use ActivityPub. For example the micro-blogging platform Mastodon and PeerTube a video hosting platform. Mastodon has millions of users. But there are still many unsolved problems in the ActivityPub world. One of them is, that the actors (user) ID is tight to there server. An user ID is an uri (mostly HTTPS) to there actor object. Because of that an actor can not change its server, without loosing its identity.

There are multiple response for an actor to want to change there server. Moderation is another unsolved problem in the ActivityPub Eco System. Many servers experiment with different approaches of moderating. Mostly they use server black or white listing. An actor that dose not like there severs moderation policy might want to change there server.
ActivityPub server are mostly operated by people in there free time. Especially smaller instances can have problems finding an new operator. If an instance goes down all users need to create a new identity on another instance and lose all there connections to other actors. This might also be a reason why most people deice to join a big instance.
The majority of all mastodon users is on a few big instances. That is a bad for decentralization. Giving actors the option to change there server, might help user to distributing user more evenly. If they do not have to fear to lose there identity on a small instance. It would also allow users already using an big ActivityPub instance, to switches to a smaller one.
    
To provide the ability to change the server, ActivityPub needs an Actor ID which is not linked to a specific server. One solution would be an decentralized or distributed ID. Decentralized Identifiers is an w3c standard (Working Draft), specifying such an ID.
Decentralized Identifiers species an decentralized Identifiers the DID (Decentralized Identifiers). A DID consists of a method and an method specific ID. The method species the method specific IDs resolution process. Methods often use distributed ledgers as a key value store. A DID can be resolved to an DID document. The DID document contains information to authenticate and verify the DID subject. A DID document can also specify services. Services are methods to communicate or interact with the DID subject. This can be an URI pointing to a website or a mail-to URI. But it also could be a URI pointing to an ActivityPub Actor Object.
### Objective
The objective is to extent ActivityPub with w3c DID, to allows actors to changes servers, without losing there identity. The protocol extension should be optional backwards compatible.
In the Bachelor Theses i will specify this extension and implement a prototype reference server and a prototype reference client.
The prototype reference client has no UI, only an API.
#### Requirements
To fulfill the objective at least these requirements need to be met:
1. A server change should have following properties:
    1. Actor B has seen, actor A before its server change. Then actor B must be able to determent, that an actor from a different server, is actually actor A.
    2. If actor A changes the server, it must not lose its Followers Collection. Activities to actor A´s Followers Collection must be delivered correctly. (So Activities from actor A to its followers are delivered correctly. Also Activities form actor B to actor A´s followers are delivered correctly.)
    3. If §actor B changes the server, it must not lose its Following Connections. So Activities from actor B, which actor A follows, to actor B´s followers, will be delivered correctly to actor A. Activities from another actor to §actor B´s followers, will be correctly delivery to actor A.
    4. Activity y from actor B should be send to actor A, because it refers to an activity X. Activity X was delivered before actor A changed the server. Activity Y must be delivered correctly to actor A. Actor A and B cloud be the same actor.
    5. If actor A changes the server, public or group accessible Activities, must stay publicly or group accessible. Like public Activities in its outbox or liked Activities.
2. The protocol extension should be compatible with non supporting clients or servers:
    1. Server A dose not support the extension. Server A must be able to communicate with clients and servers using the extension.
    2. Server A dose not support the extension. Server A must be able to preserve the extensions information. Server A can uses these information, if it is update.
    3. Server A dose not support the extension. Server A must be able to preserve the extensions information. Client of server A, which supports the extension, can use the information.
    4. Server A dose not support the extension. Client A must be able to the extensions information. So that a client from a different server can use the information.
    1. Client A dose not support the extension. Client A must be able to communicate with clients and servers using the extension.
    1. Client A dose not support the extension. Client A must be able to preserve the extensions information. Client A can uses these information, if it is update.
    1. Client A dose not support the extension. Client A must be able to preserve the extensions information. Client of server A, which supports the extension, can use the information.
    1. The protocol extension must not introduce significant latency. (yeah - know that a metric is missing)
#### Tests
To validate if the protocol extension meets the requirements, the prototype reference implementation is tested.
The test setup consists of multiple servers and clients. For most test there is the actors original server, the server the actor changes to and an third uninvolved server. Every actor has its own client. The clients are controlled by an API. 
Servers and Clients communicate over a local network. There communication is typically encrypted with HTTPS, but the test setup might use unencrypted HTTP. For testing a local DID provider might be used.
The test cases are derived from the requirements. Each requirements has at least one test. Test for requirements 1. are repeated multiple times. Every time actor B uses a different server. Actor B is the actor that dose not changes the server. Actor A is the one that changes the server. Actor B uses the actors A´s original server, the server actor a changes to and the uninvolved server.
Test for requirements 1. are repeated, with actor A´s original server turned of after the server change.
### Solution
A solution consist of three parts. The first one identifies an Actor Object using a DID. The second one identifies Collections by using an ID based on the actors DID. The third part is the server change.
#### DID as Actor ID
To uses a DID as an Actor ID, it must be possible to resolve a DID to an Actor Object. This is archived by adding an Service Endpoint to the DID document. The Service Endpoint contains the Actor Objects URI.
The DID Actor ID can be resolved to the Actor Object URI with standard DID tooling. The Actor Object can then be retrieved with an URI specific method (e.g HTTPS).
#### Collection ID
To be able to use Collections after a server change. The Collection ID need to be tight to the users identity. Therefore we need a custom URI , which is base on the Actors DID.
I have three ideas how to solve this. 
##### Method 1 - JSON-LD path URI 
Collections are identified by a custom URI. The URI is based on the DID. And resolves to the Collections URI. (The Collections ID if our extension, would not be use) 
An Collections can be located at an arbitrarily URI. The URIs structure and format can change form implementation to implementation. Therefore the URI can not be resolved by any mapping scheme.
The URIs path is a JSON-LD path. It points to a location in the Actor Object where the Collection URI can be found.
This method can only resolve Collections, which are part of the Actor Object.
##### method 2 - HTTPS with DID
Collections can be represented by a custom URI. It is based on the DID. The custom URI basically extends HTTPS. To allow a DID as host in an HTTPS URI.
A Service Endpoint in a DID document, is used to resolve the DID to an IP address.
This method would require the all implementations to use the same URI schema.
##### method 3 - an ActivityPub object identifier
Collections can be represented by a custom URI. The URI consists of a DID and an Object ID (string). 
A mapping from the custom URI to an specific HTTPS URI is possible. This is technically used to retrieved a Collection. The resolved HTTPS URI should not be used on its own.
This method uses URIs with no features. This dose not allow different implementations to use different URIs. But other extension might need to extend this URI schema.
#### Server Change
To change the server all actor information need to be copied and the DID document must be updated.
A server change is carried out by the client. The client creates an Actor Object and all Collections, it wants to keep, on the new server.
The client may use objects form its local cache, if the original server is unavailable. If successful the client can update its DID  document, with the new Actor Object Uri. Then the client should delete its Actor Object on the original server.
If the new server needs registration, the client needs to register first. Authentication and registration is not part of this extension.
## Accept v3
https://www.overleaf.com/2641456643tgwbmyxrknhq