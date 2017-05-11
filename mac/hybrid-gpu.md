
`wget https://github.com/0xbb/apple_set_os.efi/releases/download/v1/apple_set_os.efi`
#mount EFI volume to /boot/efi (if not already mounted)
`mkdir /boot/efi/custom`
`cp apple_set_os.efi /boot/efi/custom`


`/etc/grub.d/40_custom` :

```
set root='hd0,gpt1'
if [ x$feature_platform_search_hint = xy ]; then
  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1  67E3-17ED
else
  search --no-floppy --fs-uuid --set=root 67E3-17ED
fi
chainloader (${root})/EFI/custom/apple_set_os.efi
boot 
```

`sudo grub-mkconfig -o /boot/grub/grub.cfg`
