[![Logo](http://rclone.org/img/rclone-120x120.png)](http://rclone.org/)

[Website](http://rclone.org) |
[Documentation](http://rclone.org/docs/) |
[Contributing](CONTRIBUTING.md) |
[Changelog](http://rclone.org/changelog/) |
[Installation](http://rclone.org/install/) |
[Forum](https://forum.rclone.org/)
[G+](https://google.com/+RcloneOrg)


[![Build Status](https://travis-ci.org/ncw/rclone.svg?branch=master)](https://travis-ci.org/ncw/rclone) [![Windows Build Status](https://ci.appveyor.com/api/projects/status/github/ncw/rclone?branch=master&passingText=windows%20-%20ok&svg=true)](https://ci.appveyor.com/project/ncw/rclone) [![GoDoc](https://godoc.org/github.com/ncw/rclone?status.svg)](https://godoc.org/github.com/ncw/rclone) 

Rclone is a command line program to sync files and directories to and from

  * Google Drive
  * Amazon S3
  * Openstack Swift / Rackspace cloud files / Memset Memstore
  * Dropbox
  * Google Cloud Storage
  * Amazon Drive
  * Microsoft One Drive
  * Hubic
  * Backblaze B2
  * Yandex Disk
  * SFTP
  * The local filesystem

Features

  * MD5/SHA1 hashes checked at all times for file integrity
  * Timestamps preserved on files
  * Partial syncs supported on a whole file basis
  * Copy mode to just copy new/changed files
  * Sync (one way) mode to make a directory identical
  * Check mode to check for file hash equality
  * Can sync to and from network, eg two different cloud accounts
  * Optional encryption (Crypt)
  * Optional FUSE mount

See the home page for installation, usage, documentation, changelog
and configuration walkthroughs.

  * http://rclone.org/

License
-------

This is free software under the terms of MIT the license (check the
COPYING file included in this package).

S3 Setup
--------

1. As per this somewhat outdated [blog post](https://aws.amazon.com/blogs/aws/archive-s3-to-glacier/) setup a bucket in the Oregon region:
    1. Lifecycle rule:
        * Name: "Archive to Glacier"
        * Target: whole bucket
        * Action on Objects: "Archive to the Glacier Storage Class 1 days after the object's creation date."
        * Action on Incomplete Multipart Uploads: "End and Clean up Incomplete Multipart Uploads 7 days after an upload initiation date."
    2. Transfer Acceleration: Enable
2. Using the Windows binary checked into `/path/to/rclone/rclone.exe`, run `rclone config` to set up a new S3 remote:
    * Set the AWS keys
    * Set the region
3. Execute `rclone sync --verbose --exclude-from exclude.txt H:/path/to/folder --max-size 50M remote:<bucketname>/<path/to/folder>`:
```
cd H:\path\to\rclone
rclone sync --verbose --exclude-from exclude.txt H:/shared/digipowers --max-size 50M remote:digipowers-shared-v3/shared/digipowers
```
