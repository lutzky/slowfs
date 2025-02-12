# slowfs

slowfs simulates a slow filesystem for testing purposes. It uses builtin linux
capabilities to do so, namely [dm-delay]. This is just a convenience wrapper
around the technique shown in https://serverfault.com/a/954175.

[dm-delay]: https://docs.kernel.org/admin-guide/device-mapper/delay.html

To use, first create an image file to be mounted as a block device. For
instance, this will create a 100MiB ext4 filesystem:

```shell
sudo ./create_image slow.img 200 mkfs.ext4
```

Then mount it like so:

```shell
sudo mkdir -p /mnt/slow
sudo ./slowfs slow.img /mnt/slow
```

The image will remain mounted until you quit slowfs by typing `q`. Initially,
the filesystem does not add delay (e.g. so you can prepare the test environment
quickly). While running, slowfs will prompt for new delay values, and will
immediately change the delay to the new value.
