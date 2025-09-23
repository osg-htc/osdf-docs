# Access data using the OSDF

!!! abstract

    In this guide, you'll learn 
    
    * how to download and upload data using the Pelican CLI
    * how namespaces are used to organize the OSDF
    * how the OSDF reuses data through caching

The exercises in this guide assume that you have installed the Pelican CLI client on your device. 
If you have not, see the [Set up Pelican guide](pelican-client.md) for instructions.

## What's your namespace?

For the exercises below, you need to have "read" and "write" access to an OSDF namespace connected to CILogon.
Whoever directed you to this guide should have provided the necessary information.

If you were not directed to this guide, then the exercises almost certainly will not work.
You're welcome to read on, though!

## Upload data 

### Command syntax

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

### Test upload

- Create a test file
- Determine OSDF path
- Run command
- Creating password
- Authenticating upload
- Upload runs
- Confirm upload
- notes
    - future uploads
    - Data deletion

## Download data

### Command syntax


- Determine OSDF path (same as above)
- Run command
- Re-enter password
- Authenticating download
- Download runs
- Confirm download
- notes
    - future downloads
    - caching


