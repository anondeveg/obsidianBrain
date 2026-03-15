---
tags:
  - 1_Quick_notes
---

`qemu-system-x86_64 -cdrom ../isos/install-amd64-minimal-20251026T170339Z.iso -boot menu=on -drive file=gentoo.qcow2,format=qcow2 -drive if=pflash,format=raw,readonly=on,file=/usr/share/edk2-ovmf/x64/OVMF_CODE.fd -drive if=pflash,format=raw,file=OVMF_VARS.fd -smp sockets=1,cores=4,threads=2 -m 3G`