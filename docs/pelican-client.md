# Set up Pelican

!!! abstract

    The [Pelican Platform](https://pelicanplatform.org) is the software that powers the OSDF. 
    In this guide, you'll learn:

    * how to install the Pelican client
    * basics of using the Pelican client

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

Understanding the test command you ran above is a good introduction to how Pelican works.

### Commands

Most users will only ever use the `pelican object` set of commands.
To see all the available commands, run this:

```{ .bash .copy }
pelican object --help
```

??? info "Other `pelican` commands"

    You can see the other available sets of commands with

    ```{ .bash .copy }
    pelican --help
    ```

    **We recommend you avoid using these other commands unless you are specifically told to use one.** 
    These other sets of commands are generally used by the admins running a Pelican federation.

    If you are interested in learning more about these commands, we recommend reading the
    [Pelican docs](https://docs.pelicanplatform.org).


The most common commands you'll use are

| Command | Description
| --- | --- |
| <code><span style="color: red;"><b>pelican object ls</b></span></code> | list an object or namespace within a federation
| <code><span style="color: red;"><b>pelican object get</b></span></code> | download an object from a federation
| <code><span style="color: red;"><b>pelican object put</b></span></code> | upload an object to a federation

### The Pelican URL

You usually need to provide a "Pelican URL" that specifies the address of the object or namespace that you are interacting with. 
For objects in the OSDF, this URL has the following format:

<pre><code><span style="color: purple;"><b>osdf://</b></span><span style="color: green;"><b>/&lt;namespace&gt;/</b></span><span style="color: blue;"><b>&lt;object_name&gt;</b></span>
</code></pre>

* The <code><span style="color: purple;"><b>osdf://</b></span></code> prefix tells Pelican to use the OSDF.
* The <code><span style="color: green;"><b>/&lt;namespace&gt;/</b></span></code> part tells Pelican where to find the desired dataset(s).
* The <code><span style="color: blue;"><b>&lt;object_name&gt;</b></span></code> part tells Pelican the specific object to find.

If you are managing the data in a namespace, understanding the distinction between the namespace part and the object part is important.
But otherwise, most end users won't need to know the difference. 

### Altogether now

You now have all the pieces to understand the test command that you ran earlier:

<pre><code><span style="color: red;"><b>pelican object get</b></span> <span style="color: purple;"><b>osdf://</b></span><span style="color: green;"><b>/pelicanplatform/</b></span><span style="color: blue;"><b>test/hello-world.txt</b></span> <span style="color: black;"><b>./</b></span>
</code></pre>

* <code><span style="color: red;"><b>pelican object get</b></span></code> is used to download an object from a Pelican federation
* <code><span style="color: purple;"><b>osdf://</b></span></code> tells Pelican to use the OSDF
* <code><span style="color: green;"><b>/pelicanplatform/</b></span></code> tells Pelican to look in the `pelicanplatform` namespace
* <code><span style="color: blue;"><b>test/hello-world.txt</b></span></code> tells Pelican to look for the object named `test/hello-world.txt`
* <code><span style="color: black;"><b>./</b></span></code> tells Pelican to download the object to the current directory

??? question "What's in an (object's) name?"

    You may have noticed in the explanation that Pelican sees the object name as `test/hello-world.txt` but when you downloaded the object,
    the file was saved as `hello-world.txt`!

    While Pelican uses the bucket-object paradigm (like S3), it knows when and how to translate into the traditional directory-file paradigm
    when appropriate. In fact, at the Pelican origin serving the `pelicanplatform` namespace, the `test/hello-world.txt` object almost 
    certainly maps to a file `hello-world.txt` inside of a directory `test` in the connected data storage.

