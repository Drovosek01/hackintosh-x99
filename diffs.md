## Сравнение конфигов

На этой странице в удобном для меня виде будут конфиги из разных инструкций и репозиториев/EFI папок. Конфиги из чужих EFI отображаются в виде изменений примененных к стандартному `Sample.plist`, не считая удаления отключенных пунктов, включенных в стандартный конфиг для примера

### From dortania x99 HEDT

https://dortania.github.io/OpenCore-Install-Guide/config-HEDT/haswell-e.html

```
ACPI
    Add
        SSDT-PLUG
        SSDT-EC-USBX
        SSDT-RTC0-RANGE
        SSDT-UNC
Kernel
    Emulate
        Cpuid1Data: C3060300 00000000 00000000 00000000
        Cpuid1Mask: FFFFFFFF 00000000 00000000 00000000
    Quirks
        AppleCpuPmCfgLock
            No
        AppleXcpmCfgLock
            Yes
        AppleXcpmExtraMsrs
            Yes
        DisableIoMapper
            Yes
        LapicKernelPanic
            No
        PanicNoKextDump
            Yes
        PowerTimeoutKernelPanic
            Yes
Misc
    Boot
        HideAuxiliary
            Yes
    Debug
        AppleDebug
            Yes
        ApplePanic
            Yes
        DisableWatchDog
            Yes
        Target
            67
    Security
        AllowSetDefault
            Yes
        BlacklistAppleUpdate
            Yes
        ScanPolicy
            0
        SecureBootModel
            Default
        Vault
            Optional
NVRAM
    7C436110-AB2A-4BBB-A880-FE41995C9F82
        boot-args
            -v debug=0x100 keepsyms=1 npci=0x2000 alcid=1
        prev-lang:kbd
            en-US:0
    LegacyOverwrite
        Yes
    WriteFlash
        No
PlatformInfo
    SMBIOS - iMacPro1,1
UEFI
    ConnectDrivers
        Yes
    Drivers
        HfsPlus.efi
        OpenRuntime.efi
    APFS (для Mojave)
        Min Version
            -1
        Min Date
            -1
    Quirks
        IgnoreInvalidFlexRatio
            Yes
        UnblockFsConnect
            No
```

### EFI-HUANANZHI-X99-QD4-main

- https://github.com/luchina-gabriel/EFI-HUANANZHI-X99-QD4-2630L-RX5500XT
- Разница с Sample.plist

```
ACPI
    Add
        SSDT-EC-USBX
        SSDT-GPRW
        SSDT-HACK
        SSDT-HPET
        SSDT-PLUG
        SSDT-RTC0-RANGE
        SSDT-SBUS-MCHC
        SSDT-UNC
    Patch
        HPET _CRS to XCRS Rename (из SSDTTime)
        RTC IRQ 8 Patch
        TMR IRQ 0 Patch
        change Method(GPRW,2,N) to XPRW, pair with SSDT-GPRW.aml
Kernel
    Add
        Lilu
        NVMeFix
        RealtekRTL8111
        RestrictEvents (для MacPro7,1)
        USBMap
        VirtualSMC
        WhateverGreen
        AppleALC
        CpuTscSync
        SMCProcessor
        SMCSuperIO
    Emulate
        Cpuid1Data: C3060300 00000000 00000000 00000000
        Cpuid1Mask: FFFFFFFF 00000000 00000000 00000000
    Quirks
        AppleXcpmExtraMsrs
            Yes
        AppleXcpmForceBoost
            Yes
        DisableIoMapper
            Yes
        PanicNoKextDump
            Yes
        PowerTimeoutKernelPanic
            Yes
    Scheme
        KernelArch
            x86_64
Misc
    Boot
        PickerMode
            External
        PollAppleHotKeys
            Yes
        Timeout
            3
    Debug
        DisableWatchDog
            Yes
        SysReport
            Yes
    Security
        AllowSetDefault
            Yes
        ExposeSensitiveData
            3
        ScanPolicy
            2687747
        SecureBootModel
            Default
        Vault
            Optional
NVRAM
    7C436110-AB2A-4BBB-A880-FE41995C9F82
        boot-args
            keepsyms=1 debug=0x100 npci=0x2000 agdpmod=pikera
        prev-lang:kbd
            en-US:0
    LegacyOverwrite
        Yes
    WriteFlash
        No
PlatformInfo
    SMBIOS - MacPro7,1
UEFI
    Audio
        AudioOutMask
            -1
        AudioSupport
            Yes
    Drivers
        AudioDxe.efi
        HfsPlus.efi
        OpenCanopy.efi
        OpenRuntime.efi
        ResetNvramEntry.efi
    Quirks
        IgnoreInvalidFlexRatio
            Yes
```

### OC_0.8.6-RX6600_Ventura_EFI
  - https://github.com/Andrej-Antipov/X99-K9-Machinist-Hackintosh
  - Разница с Sample.plist

```
ACPI
    Add
        SSDT-PLUG-DRTNIA
        SSDT_FAKELPC
        SSDT-RTC0-RANGE-HEDT
        SSDT-UNC0
        SSDT-EC-DESKTOP
        SSDT-USBX
        SSDT-SAT1
        SSDT-MCHC
        SSDT-HPET-NEW
        SSDT-BRG0
    Patch
        SIO1 to PDRC
        XTRA to LDRC
        _SUN to XSUN
        _DSM to XDSM
        SMBS to SBUS
        EVS0 to SAT0
        FPU to MATH
        PIC to IPIC
        TMR to TIMR
        LPC0 to LPCB
        _CRS to XCRS
        RTC IRQ 8 Patch
        TMR IRQ 0 Patch
Kernel
    Add
        Lilu
        NVMeFix
        RealtekRTL8111
        USBPorts
        VirtualSMC
        WhateverGreen
        AppleALC
        CpuTscSync
        SMCProcessor
        SMCSuperIO
        XHCI-unsupported
        AirportBrcmFixup
        AirportBrcmFixup.kext/Contents/PlugIns/AirPortBrcmNIC_Injector.kext
        RadeonSensor
        SMCRadeonGPU
    Emulate
        Cpuid1Data: C3060300 00000000 00000000 00000000
        Cpuid1Mask: FFFFFFFF 00000000 00000000 00000000
    Patch
        Disable RTC wake scheduling
    Quirks
        AppleCpuPmCfgLock
            Yes
        AppleXcpmCfgLock
            Yes
        AppleXcpmExtraMsrs
            Yes
        DisableIoMapper
            Yes
        PanicNoKextDump
            Yes
        PowerTimeoutKernelPanic
            Yes
        XhciPortLimit
            Yes
    Scheme
        KernelArch
            x86_64
Misc
    Boot
        PickerMode
            External
        Timeout
            15
    Debug
        DisableWatchDog
            Yes
    Security
        AllowSetDefault
            Yes
        ExposeSensitiveData
            15
        Vault
            Optional
    Serial
        Custom
            <Some data>
NVRAM
    7C436110-AB2A-4BBB-A880-FE41995C9F82
        boot-args
            npci=0x2000  -v debug=0x100 keepsyms=1 agdpmod=ignore
        csr-active-config
            AQIAAA== (01020000)
        prev-lang:kbd
            ru:252
    Delete
        4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14
            BridgeOSHardwareModel
        7C436110-AB2A-4BBB-A880-FE41995C9F82
            csr-active-config
    LegacyOverwrite
        Yes
    WriteFlash
        No
PlatformInfo
    SMBIOS - iMacPro1,1
UEFI
    Audio
        AudioOutMask
            -1
        AudioSupport
            Yes
    Drivers
        HfsPlus.efi
        OpenCanopy.efi
        OpenRuntime.efi
    APFS (для Mojave)
        Min Version
            -1
        Min Date
            -1
    Output
        UIScale
            -1
    ProtocolOverrides
        HashServices
             Yes
    Quirks
        IgnoreInvalidFlexRatio
            Yes
```

Вопросы:
1. Зачем включен квирк XhciPortLimit? На dortania писали, что он некорректно работает на macOS 11.3+
2. Зачем патч Disable RTC wake scheduling
3. Зачем в пункте Serial добавлены данные? У вас есть COM (Serial) порт на материнской плате и вы его как-то используете? (Если да, то для чего вы его используете, если не секрет)
4. Зачем в NVRAM -> Delete -> 4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14 и 7C436110-AB2A-4BBB-A880-FE41995C9F82 добавлены пункты BridgeOSHardwareModel и csr-active-config?

https://www.applelife.ru/threads/machinist-x99k9-v2.2948848/page-30#post-1022918

### efi-machinist-x99-rs9-xeon-e2673-v3-rx570-main

   - https://github.com/gsantos022/efi-machinist-x99-rs9-xeon-e2673-v3-rx570
   - Разница с Sample.plist

```
ACPI
    Add
        SSDT-EC
        SSDT-HPET
        SSDT-PLUG
        SSDT-RTC0-RANGE
        SSDT-UNC
    Patch
        HPET _CRS to XCRS
        RTC IRQ 8 Patch
        RTC IRQ 0 Patch
Kernel
    Add
        Lilu
        NVMeFix
        RealtekRTL8111
        USBPorts
        VirtualSMC
        WhateverGreen
        AppleALC
        CpuTscSync
        SMCProcessor
        SMCSuperIO
        XHCI-unsupported
        AirportBrcmFixup
        AirportBrcmFixup.kext/Contents/PlugIns/AirPortBrcmNIC_Injector.kext
        RadeonSensor
        SMCRadeonGPU
    Emulate
        Cpuid1Data: C3060300 00000000 00000000 00000000
        Cpuid1Mask: FFFFFFFF 00000000 00000000 00000000
    Quirks
        AppleXcpmExtraMsrs
            Yes
        DisableIoMapper
            Yes
        PanicNoKextDump
            Yes
        PowerTimeoutKernelPanic
            Yes
    Scheme
        KernelArch
            x86_64
Misc
    Boot
        HideAuxiliary
            False
        PickerMode
            External
        Timeout
            3
    Debug
        DisableWatchDog
            Yes
        LogModules
            <empty string>
    Security
        AllowSetDefault
            Yes
        ExposeSensitiveData
            15
        ScanPolicy
            0
        Vault
            Optional
    Serial
        Custom
            <Some data>
NVRAM
    7C436110-AB2A-4BBB-A880-FE41995C9F82
        boot-args
            npci=0x2000 
        prev-lang:kbd
            en-US:0
    Delete
        4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14
            UIScale
    LegacyOverwrite
        Yes
    WriteFlash
        No
PlatformInfo
    SMBIOS - iMacPro1,1
UEFI
    Drivers
        AudioDxe.efi
        HfsPlus.efi
        OpenCanopy.efi
        OpenRuntime.efi
    Quirks
        IgnoreInvalidFlexRatio
            Yes
```

### Мой конфиг:

- Разница с Sample.plist
- Для дебаг версии

```
ACPI
    Add
        SSDT-UNC
        SSDT-RTC0-RANGE-HEDT
        SSDT-EC-USBX-DESKTOP
        SSDT-PLUG-DRTANIA
        SSDT-USB-Reset
    Quirks
        ResetLogoStatus
            No (убирает логотип материнке при запуске Windows)
Kernel
    Add
        Lilu.kext
        VirtualSMC.kext
        WhateverGreen.kext
        AppleALC.kext
        RadeonSensor.kext
        SMCRadeonGPU.kext
        SMCProcessor.kext
        SMCSuperIO.kext
        FeatureUnlock.kext
        CpuTscSync.kext
        NVMeFix.kext
        RealtekRTL8111-v2.2.2.kext
            MaxKernel
                18.9.9
        RealtekRTL8111.kext
            MinKernel
                19.0.0
        AirportBrcmFixup.kext
            MinKernel
                19.0.0
        AirportBrcmFixup.kext/Contents/PlugIns/AirPortBrcmNIC_Injector.kext
            MinKernel
                19.0.0
    Emulate
        Cpuid1Data: C3060300 00000000 00000000 00000000
        Cpuid1Mask: FFFFFFFF 00000000 00000000 00000000
    Quirks
        AppleXcpmCfgLock
            Yes (если не отключен MSR Lock в BIOS/UEFI)
        AppleXcpmExtraMsrs
            Yes
        CustomSMBIOSGuid
            Yes
        DisableIoMapper
            Yes
        PanicNoKextDump
            Yes
        PowerTimeoutKernelPanic
            Yes
Misc
    Boot
        HideAuxiliary
            No
        LauncherOption
            Full
        PickerMode
            External
    Debug
        AppleDebug
            Yes
        ApplePanic
            Yes
        DisableWatchDog
            Yes
        Target
            67
    Security
        AllowSetDefault
            Yes
        ScanPolicy
            0
        SecureBootModel
            Disabled
        Vault
            Optional
NVRAM
    7C436110-AB2A-4BBB-A880-FE41995C9F82
        boot-args
            alcid=7 -v keepsyms=1 debug=0x100 npci=0x2000
        csr-active-config
            FF0F0000 (или 0x285 для работы VoodooHDA)
PlatformInfo
    SMBIOS - iMacPro1,1
    UpdateSMBIOSMode
        Custom
UEFI
    APFS (для Mojave)
        Min Version
            -1
        Min Date
            -1
    Drivers
        OpenRuntime.efi
        OpenCanopy.efi
        HfsPlus.efi
        OpenLinuxBoot.efi
        ext4_x64.efi
        CrScreenshotDxe.efi
        ResetNvramEntry.efi
    Quirks
        IgnoreInvalidFlexRatio
            Yes
```