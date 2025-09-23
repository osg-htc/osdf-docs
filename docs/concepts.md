# OSDF Concepts

!!! abstract

    In this guide, you'll learn 
    
    * about
    * about

## Caching and immutability

## About namespaces

Data available via the OSDF is organized by "namespace".\*
A namespace represents a set of data connected to the OSDF.

### Access policies

Each namespace has its own set of policies controlling who can access the connected data and how it can be accessed.
The namespace and its policies are centrally registered when the data storage is connected to the OSDF.
Furthermore, 
These policies apply to any connected data that share the same prefix as the namespace.

For example, the namespace `osdf:///pelicanplatform

??? note "\*Technically, a namespace prefix"

    A Pelican Federation provides a single namespace through which connected data can be accessed.
    When data is connected to a Federation, the data has to be registered as a subset of this namespace.
    In doing 

