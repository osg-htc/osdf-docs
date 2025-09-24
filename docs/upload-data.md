# Upload data using the OSDF

!!! abstract

    In this guide, you'll learn 
    
    * something
    * something
    * something

The exercises in this guide assume that you have installed the Pelican CLI client on your device. 
If you have not, see the [Set up Pelican guide](pelican-client.md) for instructions.

## What's your namespace?

For the exercises below, you need to have "write" access to an OSDF namespace connected to CILogon.
Whoever directed you to this guide should have provided the necessary information.

If you were not directed to this guide, then the exercises almost certainly will not work.
You're welcome to read on, though!

## Command syntax

To upload data, use the `pelican object put` command.
The syntax is

```term
pelican object put <local_object> <osdf_path>
```

where `<local_object>` is the name or path to a file on your device,
and `<osdf_path>` is the location in the OSDF that you want others to use to download your data.

For example, the following command would upload the contents of `test.txt` and make it available under the address of `osdf:///pelicanplatform/test/test.txt`:

```term
pelican object put test.txt osdf:///pelicanplatform/test/test.txt
```

To run this command, you must verify with the OSDF that your identity has permission to add data to the specified namespace.
See [About namespaces](concepts.md#about-namespaces) to learn more about permissions.

## Setup test upload

First, create a file to upload as a test.

* Using a Linux or Mac terminal, run

    ``` { .bash .copy }
    echo "Testing upload to the OSDF" > upload-test.txt
    ```

* Using a Windows Powershell terminal, run

    ``` { .powershell .copy }
    notepad.exe upload-test.txt
    ```

    to launch the text editor.
    Add the desired contents, save, then close.

Next, decide on where in your OSDF namespace you want to make the file available.

* use a `test/` prefix within your namespace
* use some form of versioning in the object name

For example:

``` { .text .copy }
osdf:///YOUR_NAMESPACE/test/upload-test.01.txt
```

??? tip "Why use versioning in the name?"

    This is largely due to the caching system used by the OSDF - the system assumes that the object in the cache is the same as the object in the origin for a given address. 

    **If you upload a different object to the same OSDF address**, a client that tries to download the object could receive

    * the old version from a cache
    * the new version from the origin
    * some combination inbetween (!)

    For more information, see [Caching and immutability](concepts.md#caching-and-immutability).

## Test upload #1

Now that you are ready, run the following command:

```{ .term .copy }
pelican object put upload-test.txt osdf:///YOUR_NAMESPACE/test/upload-test.01.txt
```

!!! warning

    Make sure you change `YOUR_NAMESPACE` to **your** namespace!

    Otherwise, you'll get an error like this:

    ```{ .term .wrap }
    ERROR[2025-09-24T16:28:56-05:00] error while querying the director at
     https://osdf-director.osg-htc.org: 404: No sources found for the requested path:
     no origins found for the requested namespace '/YOUR_NAMESPACE/test/upload-test.01.txt':
     Request ID: 7f9e370a-98a0-41db-801b-5c3fd42791d1
    ```


- Authenticating upload
- Creating password
- Upload runs
- Confirm upload
- notes
    - future uploads
    - Data deletion
