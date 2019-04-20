# archiso-secure-boot

This tool allows you to sign an archiso with your secure-boot key.

## Dependencies

You need to install these dependencies first:

	pacman -S binutils sbsigntools archiso

## Build

You can easily build a signed iso with running the following command:

	./build.sh -v

The iso will be located in `out/`.

## Configuration

The following settings are available:
* Locations of the secure-boot keys
* Boot splash image
* efistub to use (e.g. for x86_32)
* gpg_key to verify image ⚠️ **Note**: this needs to be specified, otherwise
the image will refuse to boot. The key needs to be in your gnupg keychain.

Edit the file `config` to change the settings.

## Security

* The kernel command line, initramfs and boot splash will be embedded in
the signed UEFI image.
* A root password is set.
* The initramfs of arch linux does not support authentication. The
interactive shell (in case of errors) is deactivated.
* The root partition will be checked with a sha512sum (signed in the kernel
command line) and a gpg-key (signed in the initramfs).

## Known issues

* Aborting the password query results in an endless loop.

## TODO

* Add authentication method to the initramfs.
* Create a seperate hook for verifying the image.

## Related resources

* https://wiki.archlinux.org/index.php/Unified_Extensible_Firmware_Interface
* https://wiki.archlinux.org/index.php/Secure_Boot
* https://www.rodsbooks.com/efi-bootloaders/index.html
* https://bentley.link/secureboot/
