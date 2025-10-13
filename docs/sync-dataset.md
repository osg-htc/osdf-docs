# Sync your dataset using OSDF

!!! abstract

    In this guide, you'll learn

    * how to upload your dataset to the OSDF
    * how to download your dataset from the OSDF

This guide assumes that you have installed the Pelican CLI client on your device.
If you have not, see the [Set up Pelican guide](pelican-client.md) for instructions.

Furthermore, this guide assumes that you have completed one or both of the [Upload data guide](upload-data.md) and the [Download data guide](download-data.md).

## The sync command

The Pelican client provides the command `pelican object sync` for handling the transfers of many objects.
The syntax for the command is:

```{ .term }
pelican object sync <source> <destination>
```

where one of `<source>` and `<destination>` is a directory on your local device and the other is the OSDF address you want to sync against.
These references can be individual objects, but the command is best suited for many objects.

The sync command will act **recursively**. 
If uploading a local directory that in turn contains additional directories with files, the whole directory tree will be reproduced under the OSDF address you specified.
If downloading objects from an OSDF address, the client will download all objects that share the same OSDF address as their prefix.

If the transfer is interrupted, you can rerun the same `pelican object sync` command and it will skip objects that were already successfully transferred.

## Using the sync command to upload data

If the destination for the `pelican object sync` command is an OSDF address, then the client will upload the **contents** of the local directory you provided to the corresponding object store.

```{ .term .copy }
pelican object sync LOCAL_DIRECTORY osdf:///YOUR_NAMESPACE/some_location
```

!!! warning

    The emphasis on "contents" is because the name of the local directory will **not** be automatically included in the OSDF address for the objects you upload.
    In this example, that means the OSDF address you choose will not automatically include the name of `LOCAL_DIRECTORY` in the prefix.

    If you want that name to be included in the prefix, then you need to include it in the OSDF address you specify!

Like with [uploading a single object](upload-data.md), you will need to authenticate your identity to provide the necessary authorization.
Once authorized, the client will recursively upload the contents of the local directory.

**The sync command will not overwrite existing objects on upload!**

!!! bug

    Currently there is a bug where uploading a directory with object names that already exist at the OSDF address will return a `403 forbidden` error.
    The client will still attempt to upload any of the new objects it found in the local directory, but even if that is successful the command will overall return the `403 forbidden` error.

    For updates, see the [bug report](https://github.com/PelicanPlatform/pelican/issues/2735).

### Setup test upload sync

On your local device, create the following directory tree:

```
sync-test.01/
├── nested/
│   └── nested.txt
└── test.txt
```

You can recreate this structure by copying and running the following commands (Linux/Mac):

```{ .bash .copy }
mkdir -p sync-test.01/nested
echo "First file in the sync test" > sync-test.01/test.txt
echo "Second file (nested) in the sync test" > sync-test.01/nested/nested.txt
```

If using Windows PowerShell, use the File Explorer to create the directories and Notepad or other text editor to create the files.

??? tip "Why is there a number in the names?"

    A major assumption of the OSDF (and the Pelican software that backs it) is that the objects it makes accessible
    are **immutable**, that is, they **do not change**.

    Here, the number is provided as a way to version the name of the objects. 

    To repeat this exercise (after the `sync-test.01` files have been uploaded), you can just increment the number to try again.

    For more information, see the section on [Caching and immutability](concepts.md#caching-and-immutability).

Next, identify the OSDF address that you want to make the **contents** of the local directory available at. 
We recommend using `osdf:///YOUR_NAMESPACE/test/sync-test.01`.

### Test upload sync

Make sure that your terminal is in the directory that contains the `sync-test.01` folder.
Then run

```{ .term .copy }
pelican object sync sync-test.01 osdf:///YOUR_NAMESPACE/test/sync-test.01
```

Remember that the `sync` command will upload the **contents** of the local directory - if you want to have the local directory name `sync-test.01` in the final OSDF address, then you need to include it in the OSDF address you are uploading to.

You will be prompted to authenticate, just like you did in the [Upload data test](upload-data.md#authenticate-upload).
Once you've secured the necessary authorization, the upload should be brief.

??? tip "In case of errors"

    If the upload of one of the objects encounters an error, the corresponding error message should be printed and in most cases the client will continue with uploading the other remaining objects.
    
    If you try the sync command again, it should skip the objects that were successfully uploaded.

    For assistance in troubleshooting an error, consider reaching out to <a href="mailto:support@osg-htc.org">support@osg-htc.org</a>.

### Confirm uploads

To confirm that the upload was successful, check that the objects can now be listed.

First, run this command to check the available objects under the OSDF address you provided for the sync command:

```{ .term .copy }
pelican object ls -l osdf:///YOUR_NAMESPACE/test/sync-test.01
```

You should see two new items in this listing: `test.txt` and `nested`.
If there are no other objects under your `test` prefix, the output would look like this:

```{ .term }
/YOUR_NAMESPACE/test/sync-test.01/nested      0   2025-10-10 21:10:32
/YOUR_NAMESPACE/test/sync-test.01/test.txt   28   2025-10-10 21:10:32
```

The entry for `nested` lists 0 bytes (middle column), which is an indication that this is not an object but rather an extension of the OSDF address.
Take a look at the objects available under the nested address with 

```{ .term .copy }
pelican object ls -l osdf:///YOUR_NAMESPACE/test/sync-test.01/nested
```

This time, you should only see one entry listed corresponding to `nested.txt`:

```{ .term }
/YOUR_NAMESPACE/test/sync-test.01/nested/nested.txt   34   2025-10-10 21:10:32
```

!!! tip

    To further confirm that your data was successfully synced to the remote object store in the OSDF, follow the instructions in the next section to download the objects and inspect their contents.

## Using the sync command to download data

If the source is an OSDF address, then the client will download all objects that share the same OSDF prefix as the address to the local destination that you specified.
This will reproduce directories in the local file system that corresponds to the nesting of the object addresses.

```{ .term .copy }
pelican object sync osdf:///YOUR_NAMESPACE/some_prefix NEW_LOCAL_DIRECTORY
```

!!! danger "Careful!"

    The sync command will **overwrite** any local objects that have the **same name** but **different contents** when downloading!
    
    Local objects with different names will be unaffected, even if inside of a sub-directory created by the sync command.

Like with [downloading a single object](download-data.md), the OSDF address you are trying to access may require that you authenticate your identity to provide the necessary authorization for downloading the data.

### Setup test download sync

On your local device, create a new empty directory and move into it:

```{ .term .copy }
mkdir sync-download-test
cd sync-download-test
```

The instructions below assume that the namespace has the addresses created in the [section above](#using-the-sync-command-to-upload-data): `osdf:///YOUR_NAMESPACE/test/sync-test.01`.

**If your namespace does not have this address**, then 

* If you have upload permissions, we recommend that you first complete the [exercises above](#using-the-sync-command-to-upload-data)!

* If you do **not** have upload permissions, we recommend that you first finish reading this guide.
  Then try to apply your understanding to a "small" sync of data from your namespace.

### Test download sync

Inside the empty directory, run the following command: 

```{ .term .copy }
pelican object sync osdf:///YOUR_NAMESPACE/test/sync-test.01 ./
```

You will be prompted to authenticate, just like you did in the [Download data test](download-data.md#authenticate-upload).
Once you've secured the necessary authorization, the download should be brief.

??? tip "In case of errors"

    If the download of one of the objects encounters an error, the corresponding error message should be printed and in most cases the client will continue with download the other remaining objects.
    
    If you try the sync command again, it should skip the objects that were successfully downloaded.

    For assistance in troubleshooting an error, consider reaching out to <a href="mailto:support@osg-htc.org">support@osg-htc.org</a>.

### Confirm downloads

After the `sync` command finishes, list the contents of your current directory with

```{ .term .copy }
ls
```

You should see the file `test.txt` and a directory `nested`. 
Again, this is because the `sync` command transfers the **contents** of the address you specified.

??? tip "Creating `sync-test.01`"

    If you want the sync command to put the contents into a new local directory `sync-test.01`, then you can use this command instead:

    ```{ .term .copy}
    pelican object sync osdf:///YOUR_NAMESPACE/test/sync-test.01 ./sync-test.01
    ```

Using your terminal or your device's file explore, confirm that the `sync` command created the following structure, files, and contents:

```
./
├── nested/
│   └── nested.txt   # Contains "First file in the sync test"
└── test.txt         # Contains "Second file (nested) in the sync test"
```

??? example "Overwriting local objects"

    As warned above, the sync command will overwrite any local objects with the same name/path as the object you are downloading.
    To see this in action, try the following:

    1. Edit the contents of `sync-download-test/test.txt`  using your terminal or device's text editor.
    2. Create or copy files to `sync-download-test/test2.txt` and `sync-download-test/nested/nested2.txt`.
    3. In the parent `sync-download-test` directory, rerun the same `pelican object sync` command that you did in [Test download sync](#test-download-sync).
    
    Now check the results:
    
    * Did your changes to `test.txt` persist?
    * Were your new files `test2.txt` and `nested2.txt` affected?

