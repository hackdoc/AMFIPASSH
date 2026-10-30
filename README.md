# AMFIPASSH

Releases for AMFIPassH. Each release provides:

- `AMFIPassH-kext.zip`: `AMFIPassH.kext`
- `AMFIPASSH-Monitor.zip`: `AMFIPASSH Monitor.app`

## Install the kext

1. Download and unzip `AMFIPassH-kext.zip`.
2. Copy `AMFIPassH.kext` into `EFI/OC/Kexts`.
3. Add the entry under `Kernel -> Add` in the OpenCore config, after Lilu.
4. Set `SecureBootModel` to `Disabled` and do not add any `amfi` boot argument.
5. Reboot.

## Status panel

Unzip `AMFIPASSH-Monitor.zip`, drag `AMFIPASSH Monitor.app` into `/Applications`, and open it. It shows whether the kext is loaded, the hook state and admission records, and offers a gate test and a TCC check.
