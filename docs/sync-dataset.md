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

> Globs may or may not work

