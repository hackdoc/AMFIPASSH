# AMFIPASSH

Releases for AMFIPassH. Each release provides:

- `AMFIPassH-v<version>-RELEASE.zip`: `AMFIPassH.kext`
- `AMFIPassH-v<version>-DEBUG.zip`: `AMFIPassH.kext` with extra debug symbols
- `AMFIPASSH-Monitor-v<version>.zip`: `AMFIPASSH Monitor.app`

## Install the kext

1. Download and unzip either kext archive.
2. Copy `AMFIPassH.kext` into `EFI/OC/Kexts`.
3. Add the entry under `Kernel -> Add` in the OpenCore config, after Lilu.
4. Set `SecureBootModel` to `Disabled` and do not add any `amfi` boot argument.
5. Reboot.

Use the RELEASE archive for daily use and the DEBUG archive only when troubleshooting.

## Status panel

Unzip the monitor archive, drag `AMFIPASSH Monitor.app` into `/Applications`, and open it. It shows whether the kext is loaded, the hook state and admission records, and offers a gate test and a TCC check.
