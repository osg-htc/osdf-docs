# OSDF Concepts

!!! abstract

    In this guide, you'll learn about the concepts of
    
    * namespaces, including access policies
    * caching and immutability

## About namespaces

Data available via the OSDF is organized by "namespace".
A namespace represents a set of data connected to the OSDF.

### Who owns a namespace?

Each namespace has its own set of policies controlling who can access the connected data and how it can be accessed.
The namespace and its policies are centrally registered when the data storage is connected to the OSDF.
Furthermore, these policies apply to any connected data that share the same prefix as the namespace.

For example, the namespace `osdf:///pelicanplatform` is registered by the Pelican Platform. 
They therefore control the objects and nested namespaces listed under that prefix.
A third party cannot register `osdf:///pelicanplatform/alternate`, since it contains the prefix owned by Pelican Platform.

??? question "What about data ownership?"

    The OSDF and other federations using the Pelican Platform are merely distribution systems: **the data provider maintains ownership of their data** under the data federation model.
    If the data provider limits access to their data to certain users, every component of the federation will respect those limitations.

!!! tip "Connecting data to the OSDF"

    If you have a dataset you want to make available via the OSDF, please reach out! 

    * You can [request a consultation](https://docs.google.com/forms/d/e/1FAIpQLSdr3pLLRlEbhbf-h8cdZ5N9UJpshIDdgUeHJ07keRUK8ecKOw/viewform?usp=dialog).
    * You can email us at <a href="mailto:support@osg-htc.org">support@osg-htc.org</a>.

    For more information on the OSDF, see this [overview page](https://osg-htc.org/services/osdf).

### Who can access a namespace?

Each namespace can be configured with different access policies:

* Public Read - anyone can download the data from this namespace
* Read - only authenticated users can download the data from this namespace
* Write - only authenticated users can upload data to this namespace

The entity that registered the namespace has control over how users authenticate access.
For the most part, namespaces in the OSDF use COmanage (for managing access) and CILogon (for authenticating access).

!!! tip "What's in a name?"

    Typically, the name used for the namespace suggests something about the provenance and accessibility of the data.
    For more information, see the Pelican guide on [Choosing Namespaces](https://docs.pelicanplatform.org/federating-your-data/choosing-namespaces).

If you are the manager of a namespace that was set up in coordination with the OSDF team, you can control access to your namespace following the instructions in the [Collaborator access guide](collaborators.md).

## Caching and immutability

One of the main advantages of using the OSDF is the extensive system of caches geographically distributed across North America and beyond.
Currently, in order for this system to work, the objects downloaded from the OSDF are assumed to be immutable.

### What is a "cache"?

When data is downloaded from the OSDF, it typically passes through a "cache" before reaching its final destination.
The cache keeps a copy of that data after the download is completed. 
That way, the next time someone tries to download the same data, the cache can provide its copy instead of going all the way back to the original storage system.

### Why does the OSDF use caches?

The OSDF was originally designed to support high throughput computing (HTC) workloads.
An HTC workload could be anywhere from 10 to 1,000,000+ jobs, and typically there is some files common across all jobs.
If those common files are large, an HTC workload can easily overwhelm the local network where the files are originally stored.

By using caches, the OSDF can store copies of large files in servers much closer to where the HTC jobs are actually running. 
These servers are located on internet backbones to ensure high bandwidth.
When an HTC workload is deployed, the first few downloads of the large file will populate the network of caches.
Subsequent downloads can then fetch the large file from a cache instead of the original data storage.

### Why is "immutability" important?

For this caching system to work, the OSDF assumes that the objects that are downloaded are "immutable" - that is, they do not change.
That is because when you download an object multiple times from the OSDF, you are typically downloading a copy from one of the caches.

If the object changes at the original data storage, then the copy stored at the cache no longer matches the object at the original data storage.
Now when you try to download the object, you may get the old version or the new version.
This inconsistency currently cannot be accounted for in the OSDF system and can cause problems in your work.

!!! warning "Frankenstein's objects"

    Because of some technical details with the Pelican software, if the object at the origin changes, then a client downloading the object may receive:

    * the older version of the object,
    * the new version of the object, or
    * **some combination of the old object and the new object!**

### Help, I changed the object! What do I do?

If you have to change the object at the origin, we recommend that you change the name of the object as well.
That way, its OSDF address will differ from any copies that are stored in a cache.

If you can't change the name of the object, then we recommend that you wait a couple of days before trying to download the object again.
The copies kept by the caches will be cleaned out in order to make room for other objects that are being downloaded.
(There currently isn't a mechanism within Pelican to "purge" caches of old copies of objects.)

If you need help, contact the OSDF team at <a href="mailto:support@osg-htc.org">support@osg-htc.org</a>.

!!! info "Immutability and the future of Pelican"

    A long term goal in the development of the Pelican software is to address this assumption of immutability.
    Eventually, objects in a Pelican data federation will have the concept of versioning, enabling caches to check if the copy they are storing is the most recent version.

### What about removing objects?

In principle, you can remove an object from the original data storage.
Any copies on the caches, however, will persist, at least until the cache needs to make room for more recent objects.

If you need to remove objects from your origin, we recommend contacting the OSDF team for assistance at <a href="mailto:support@osg-htc.org">support@osg-htc.org</a>.
