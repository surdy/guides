## Unable to resize partition (Assuming FileVault is Off)
This could be because the disk is a CoreStorage Volume. To verify this run

`diskutil corestorage list`

If you see Corestorage logical volumes then revert to default partition type by typing:

`diskutil corestorage revert <UUID for logical volume containing OSX>`

Now you should be able to resize the partition


##
