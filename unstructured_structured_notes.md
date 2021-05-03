+ Introduction
    + Motivation
        + kein motivation mehr
    + Anforderung / Ziel / Problem Description
+ Related Work (kann man das weg lassen)
+ Grundlagen
    + activitPub
    + ipfs
        + mutalbe vs unmutable
+ Impacet Requirements (anfoderungs analyse)
    + General
        + scalability soll nicht schlechter werden
            + fürs ganze system
            + soll fair sein für große und klein nodes
        + do not destry use case, user can be offline
    + Identity
        + impacet
        + Requirements
    + Content
        + impacet
        + Requirements
    + Social Graph
        + impacet
        + Requirements
    + Inbox Outbox
        + impacet
        + Requirements
    + Replication
+ Lösungen
    + gereral concept
        + use content addressed storage
    + Components
        + Idnentity
            + IPFS
                + problems with replication:
                    + we dont want multiple live versions
            + ~~Decentralized Id~~
        + Content
            + Mutable
            + Unmutable
            + (compate solution)
        + Social Graph
            + ~~on server (backup)~~
            + ipfs
        + Inbox Outbox
            + on server
                + becouse compatible with other ap instacnes or so
            + ipfs
                + loses many of the features ap provieds
    + Replication
+ Experiment / evaluation
    + test compoents write with only local pinning without replication. compare to http
    + test read with local, 1 remote with pinning, n remotes with pinning. and differtens sizes
    + (test on public ipfs network)
    + test primitives

    + desing
        + Identity and mutable content and immutabel content
            + how long dose it take to write content
                + without replication
                + only to localy pinned
                + (try with replication ????)
                + test on public ipfs network
                    + maximum or most realistic load for the dth
                + comper to http
            + how long dose it take to read content
                + localy pinned; pinned on n remote machines, for n > 0
                + differten sizes of content
                + make a ~1000 tests
                + every time read new random content to prevent caching, caching is on all remote machines
                + test on public ipfs network
                    + maximum or most realistic load for the dth
                + comper to http
            + further system metric
                + whiche once ????
                + on client and the other machines
                    + this cloud show us if the load is shared among remote machines or if more remote machines increates the overall kosten
                + comper to http
        + Social Graph
            + how long dose it take to read
                + localy pinned; pinned on n remote machines, for n > 0
                + differten sizes of content
                + make a ~1000 tests
                + test on public ipfs network
                    + maximum or most realistic load for the dth
                + comper to http
            + how long dose it take to update
                + without replication
                + only to localy pinned
                + (try with replication ????)
                + test on public ipfs network
                    + maximum or most realistic load for the dth
                + comper to http
            + storage used by old versions
                + create an empty collection
                + check how muche stroge is used 
                + add lods of data to the collections and remove it again
                + check how much stroge is used
                    + a replication hose can not do garbage collection
                    + this would be its status
                + check how much stroge is used after garbage collection
        + Inbox Outbox
            + how long dose it take to read the outbox/public timeline or inbox/my timeline
                + test on public ipfs network
                    + maximum or most realistic load for the dth
                + both version
                + differtens sizes
                + only mesuer time in needs to retive the links, dont resolve the links to objects, if they are not emmbedded
                + comper to http
            + how long dose it take to deliver one message
                + test on public ipfs network
                    + maximum or most realistic load for the dth
                + both version
                + comper to http
                + deliver message to one remote server, deliver message to user on local server
            + some home messure recive
                + who ?????????
        + replication
+ Discussion


+ todo:
    + did any one charactrize messure ipfs and special im- vs mutable
    + dit any one characterize activtyPub

