# Remove MacOS entries
sudo chmod -x /etc/grub.d/30_os-prober
sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg 


#
