# libreELEC-CVBS-binaries
binaries for wetek play with CVBS support

The WETEK Play - Openelec edition has a CVBS output that doesn't work anymore since [this commit](
https://github.com/OpenELEC/OpenELEC.tv/commit/ffe39368400fb58bb59541fc015e334e1eec3ed0), leaving no solution for users that rely on CVBS. (See [this issue](https://github.com/OpenELEC/OpenELEC.tv/issues/4502))

So, here are de binaries compiled from the unofficial fork of {[Open](https://github.com/rgenoud/OpenELEC.tv/tree/openelec-6.0-cvbs),[Libre](https://github.com/rgenoud/LibreELEC.tv/tree/libreelec-8.2.5-cvbs)}ELEC.

# HOWTO
## Merge / uncompress
The files are compressed and, for some, splitted (for size reasons).

So, you have to uncompress them before use (with 7zip or file-roller for instance).

For splitted files, you have to merge them before uncompressing.

**Linux**
```
cat LibreELEC-WeTek_Play.arm-8.2.5cvbs.tar.xz-part* > LibreELEC-WeTek_Play.arm-8.2.5cvbs.tar.xz
```
Then, uncompress:
```
xz -d LibreELEC-WeTek_Play.arm-8.2.5cvbs.tar.xz
```

**Windows**
```
copy /b LibreELEC-WeTek_Play.arm-8.2.5cvbs.tar.xz-part* LibreELEC-WeTek_Play.arm-8.2.5cvbs.tar.xz
```
Then, uncompress with 7zip.

## Copy the file to the Wetek Play
**Linux**
```
scp LibreELEC-WeTek_Play.arm-8.2.5cvbs.tar wetek_ip_address:/storage/.update/
ssh wetek_ip_address "echo 576cvbs > /storage/.kodi/userdata/fallback_cap"
```
Then, reboot the Wetek Play, and wait for the firmware upgrade.

**Windows**

Use putty or whatever to do the same.

# Compressing / Splitting
The files were compressed with xz, no specific option, and split like that:
```
for i in *.xz ; do split -a1 -d -n 3 "$i" "$i"-part ; done
```
