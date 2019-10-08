---
title: "Raspberry pi 3 - qemu environment"
last_modified_at: 2019-07-13T10:00:00-09:00
categories:
- OS Kernel Dev
- QEMU
tags:
- qemu
- raspberry pi
- os
excerpt: "RasPi3 qemu compile & How to use \"qemu\""
---

[qemu official][qemu]

[raspberry pi 3 support for qemu][bzt/qemu]

[compile dependency package of qemu compile][qemu compile package]

```
apt-get install build-essential zlib1g-dev pkg-config libglib2.0-dev binutils-dev libboost-all-dev autoconf libtool libssl-dev libpixman-1-dev libpython-dev python-pip python-capstone virtualenv
```


[qemu]: https://github.com/qemu/qemu
[bzt/qemu]: https://github.com/bztsrc/qemu-raspi3
[qemu compile package]: https://github.com/Cisco-Talos/pyrebox/issues/41
