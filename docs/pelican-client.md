# Set up Pelican

The [Pelican Platform](https://pelicanplatform.org) is the software that powers the OSDF. 
In this guide, you'll learn:

* how to install the Pelican client
* basics of using the Pelican client

Links to the official Pelican documentation are included throughout.

## Install the Pelican client

We recommend that you use the Pelican CLI (command line interface) client for most purposes.
To install the Pelican CLI, follow the instructions for your operating system:

* [Install Pelican CLI on Linux :material-arrow-right:](https://docs.pelicanplatform.org/install/linux-binary)
* [Install Pelican CLI on macOS :material-arrow-right:](https://docs.pelicanplatform.org/install/macos)
* [Install Pelican CLI on Windows :material-arrow-right:](https://docs.pelicanplatform.org/install/windows)

For additional ways to install the Pelican CLI client, see the [Pelican documentation](https://docs.pelicanplatform.org/install).

??? info "Other Pelican clients"

    There are other Pelican clients for interacting with Pelican federations such as the OSDF.
    For more information, see the [Pelican client documentation](https://docs.pelicanplatform.org/getting-data-with-pelican). 

    **For the purposes of this website, we assume that you are using the Pelican CLI client!**

### Confirm installation

Let's confirm you have Pelican installed by running the following command:

```{ .bash .copy }
pelican --version
```

This command should work regardless of your operating system and will display the version number,
as well as some information about the software build.

For example,

```term
$ pelican --version
Version: 7.19.2
Build Date: 2025-09-11T16:10:33Z
Build Commit: 298fba8f7a7801adc35b4a3620d117ad38bb436a
Built By: goreleaser
```

### Test download

Next, you should test that you can download a public object from the OSDF.
Run the following command:

```{ .bash .copy }
pelican object get osdf:///pelicanplatform/test/hello-world.txt ./
```

You may or may not see a progress bar as part of the download - it depends on how quickly the object can be downloaded.
For example:

```term
$ pelican object get osdf:///pelicanplatform/test/hello-world.txt ./
hello-world.txt 27.00b / 27.00b [=======================================] Done!
```

If successful, you should see a new file in your directory called `hello-world.txt`, with the following contents:

```text
If you are seeing this message, getting an object from OSDF was successful.
```

## Pelican client basics





