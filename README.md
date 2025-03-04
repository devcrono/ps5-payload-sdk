# PS5 Payload SDK
This is an SDK for developing ELF payloads targeted at exploited PS5s running
the [BD-J ELF loader][bjd-elf]. Several artifacts in this repository originate
from the [PS5SDK][PS5SDK] project.

## Prerequisites
On Debian-flavored operating systems, you can invoke the following command to
install dependencies used by the SDK.
```console
john@localhost:ps5-payload-sdk$ sudo apt-get install build-essential cmake clang clang-15 lld lld-15
```

## Building
```console
john@localhost:ps5-payload-sdk$ make
```

## Installation
```console
john@localhost:ps5-payload-sdk$ make DESTDIR=/opt/ps5-payload-sdk install
```

## Usage
```console
john@localhost:ps5-payload-sdk$ export PS5_PAYLOAD_SDK=/opt/ps5-payload-sdk
john@localhost:ps5-payload-sdk$ make -C samples/hello_world
john@localhost:ps5-payload-sdk$ export PS5_HOST=ps5; export PS5_PORT=9020
john@localhost:ps5-payload-sdk$ make -C samples/hello_world test
```

## Adding new SCE Libs
If you have decrypted sprx files that you would like to interact with, you can
build stubs for them as follows:
```console
john@localhost:ps5-payload-sdk$ sudo apt-get install wget python3 python3-pyelftools
john@localhost:ps5-payload-sdk$ cp /path/to/sprx/libSceXYZ.sprx sce_stubs/
john@localhost:ps5-payload-sdk$ make -C sce_stubs stubs
john@localhost:ps5-payload-sdk$ make DESTDIR=/opt/ps5-payload-sdk install
```

## Reporting Bugs
If you encounter problems with ps5-payload-sdk, please [file a github issue][issues].
If you plan on sending pull requests which affect more than a few lines of code,
please file an issue before you start to work on you changes. This will allow us
to discuss the solution properly before you commit time and effort.

## License
Files in the include_bsd directory are licenced under BSD licences.
Unless otherwhise explicitly stated inside a file, the rest are licensed under
the GPLv2.

[issues]: https://github.com/john-tornblom/ps5-payload-sdk/issues/new
[bjd-elf]: https://github.com/john-tornblom/bdj-sdk/tree/master/samples/ps5-payload-loader
[PS5SDK]: https://github.com/PS5Dev/PS5SDK
