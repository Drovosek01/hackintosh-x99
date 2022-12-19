Пока нет возможности вплотную заняться хакинтошем на этой платформе, поэтому статус репозитория и моего хакинтоша на x99 - WIP

## Железо:

- Процессор: Intel Xeon E5-2666 v3 (Haswell-EP)
- Видеокарта: Sapphire RX580 Nitro+ 4Gb
- ОЗУ: 64GB (16 x 4) 1600 MHz Samsung ECC Reg
- Материнская плата: Jingyue X99 Titanium D3
  - Чипсет: Intel Lynx Point B85
  - Сетевая карта: Realtek RL8168/8111 Ethernet
  - Аудио чип: ALC887
- Wifi + Bluetooth: Broadcom BCM4331 (BCM94331) 802.11n
- Накопители:
  - WD Black SN730 1TB - SSD NVMe
  - 2 Western Digital HDD
- Блок питания: Aerocool VX Plus 500
- Мониторы:
  - EnVision LCD2361 (1920x1080) - по DVI-D
  - HP Z23n (1920x1080) - по DisplayPort

## TODO:

1. Андервольтинг
   - Попробовать снизить ток процессора, чтобы увеличилась частота в рамках теплопакета
2. Разблокировка Turboboost
   - Разблокировать возможность достигать максимальной частоты при турбобусте на всех ядрах, а не только на 1 ядре
   - Наверное понадобится утилита S3TurboTool
     - https://xeon-e5450.ru/socket-2011-3/e5-2600-v3/dobavlyaem-anlok-v-bios-raz-i-navsegda-cherez-s3turbotool/
     - https://4pda.to/forum/index.php?showtopic=1015953
     - http://xeonlive.ru/instruktsii/unlock-turbo-boost-s-pomoshchyu-s3turbotool
     - https://github.com/Koshak1013/HuananzhiX99_BIOS_mods
     - https://www.youtube.com/watch?v=Oww5tTNDhsA
3. Попробовать биос Jingyue X99 Titanium D3 от "кошака"
   - При этом не забыть сделать свой дамп оригинального биоса
   - https://github.com/Koshak1013/HuananzhiX99_BIOS_mods/tree/master/Jingyue%20X99%20Titanium%20D3
4. Попробовать оживить сон на материнской плате
5. Изучить настройки биоса
   - По сравнению с моей платой на x79, на данной материнке довольно много настроек, хочется что-нибудь улучшить с их помощью
6. Увеличить частоту ОЗУ
   - В биосе можно выставить частоту ОЗУ 1867 МГц, но при запуске Windows 10 и macOS Monterey в них частота ОЗУ так и отображается на 1600 МГц. Наверное нужно в биосе в разделе настройки таймингов выбрать ручной режим и вручную их настроить
7. Настроить AppleALC
   - Тут аудио кодек ALC887 и в паре с кекстом AppleALC звук не заработал ни в каком виде, какие бы значения для кодека ALC887 я не задавал в аргументе `alcid=`
   - Вместе с VoodooHDA 3.01 удалось завести звук (работает порт как на задней, так и на передней панели), хотя с значением `0x285`, кекст не хотел появляться среди загруженных и пока полностью отключил SIP. Это удалось не с первого раза, в итоге в OpenCore Configurator для `csr-active-config` задал значение `FF0F0000` и перезагрузил со сбросом NVRAM
   - https://www.insanelymac.com/forum/topic/314406-voodoohda-302/?do=findComment&comment=2756841
   - Чтобы звук в паре с VoodooHDA заработал пришлось добавить SSDT-HDEF
8. ~~Победить странные тормоза в macOS Monterey~~
   - Иногда в macOS Monterey начинаются лаги в виде очень долгого запуска даже стандартных легких программ типа "Мониторинг системы"
   - Такая же ситуация была и на хакинтоше с x79 с этим же SSD и этой же системой
   - Переустановил начисто с macOS Monterey 12.6.1 на 12.6.2, надеюсь это поможет, но лаги непостоянные/непрогнозируемые, буду наблюдать
     - Вроде помогло
9. Выяснить почему в AmorphousMemoryMark скорость записи в ОЗУ в 2 раза меньше скорости чтения
10. Переехать на использование Clover
   - И потом сравнить результаты в бенчмарках при OpenCore и Clover
11. USB порты работают без USBInjectAll и XHCI-inject, только с SSDT-Reset-All
    - Сделать USBMap и посмотреть разницу
12. Попробовать оптимизировать DSDT разными патчами ACPI
13. Выяснить нужно ли включать VT-d и что значит появление AppleVTd в IOReg
14. Попробовать заменить кекст PMDrvr на патчи ядра
    - https://www.insanelymac.com/forum/topic/317747-haswell-e-powermanagement-yet-another-option/
    - https://www.insanelymac.com/forum/topic/341477-open-core-kernel-kext-patch-for-x99x299-motherboard/
15. Сравнить работу с CpuTscSync и с VoodooTscSync
    - В DSDT также есть лишние сокеты и ядра, как в случае с DSDT на хакинтоше на x79, но macOS Monterey запускалась без проблем. Наверное CpuTscSync как-то патчит DSDT и раз на x79 я его не использовал, пришлось вручную удалять лишние ядра и процессоры/"логические поток"

## Физическое TODO:

- Сделать коннектор с 4-пин на USB, чтобы запитать Bluetooth на комбомодуле, потому что на материнской плате только один 4-пин разъем и приходится выбирать - либо блютуз, либо USB 2.0 на передней панели

## Выявленные особенности:

1. С заметной частотой OpenCore 0.87 запускает меню (Picker) с GUI довольно долго, иногда примерно секунд 15-20, а иногда быстро 2-5 секунд.
   - Наверное это особенности Debug версии
2. При запуске OpenCore 0.87 Debug с включенными всеми дебаг квирками и аргументами ядра, буквы перед появлением меню (Picker) довольно большие
   - Но при использовании релиз версии и отключением дебаг квирков и аргументов загрузки, надеюсь, это не будет проблемой
3. Скорость перемещения курсора в меню OpenCore 0.87 Debug довольно медленная, точнее курсор лагает, но это пустяк
4. Иногда при запуске macOS Monterey появлялась паника ядра на строке `proc_pidpathinfo_internal : EACCESS returned by vnode_lookup for pid 241`
   - https://www.applelife.ru/threads/opencore-obsuzhdenie-i-ustanovka.2944066/page-806#post-1022916
5. При добавлении SSDT-PLUG (с dortania), управление питанием процессора работает без проблем на первый взгляд, но если запускать многопоточную нагрузку (например в Cinebench R23), то средняя частота ядра не поднимается выше 2,5 ГГц. Проблема решается использованием кекста PMDrvr, либо включением квирка `AppleXcpmForceBoost`
   - Но при использовании квирка `AppleXcpmForceBoost` процессор, по первым ощущениям, реже опускается к низким частотам и в Intel Power Gadget в пункте Core Req указывается 25,5 ГГц
   - https://www.applelife.ru/threads/machinist-x99k9-v2.2948848/page-30#post-1023013
6. Для того, чтобы запустилась macOS Mojave помимо задания значения `-1` для пунктов `MinDate` и `MinVersion` нужно еще выставить значение `Disabled` для пункта `SecureBootModel`
   - Иначе будет остановка на строке `oscb no suitable signature`
   - https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/extended/kernel-issues.html#stuck-on-ocb-loadimage-failed-security-violation
7. В BIOS/UEFI есть пункт `MSR Lock Control` и изменение значения на `Disable` (изначально стоит `Enable`), позволяет не включать квирки `AppleCpuPmCfgLock` и `AppleXcpmCfgLock`
   - В BIOS/UEFI при выделении этого пункта сбоку написано "Enable - MSR 3Ah, MSR 0E2h and CSR 80h will locked. Power Good reset needed to remove lock bits"
8. Без использования квирка `AppleXcpmExtraMsrs` macoS Monterey не грузится
9. Столкнулся с той же проблемой, что и на платформе x79. При запуске Windows - она запускается только с 4 раза если запускать ее после перезапуска из macOS
   - https://github.com/acidanthera/bugtracker/issues/2184
   - https://applelife.ru/threads/opencore-obsuzhdenie-i-ustanovka.2944066/page-806#post-1023286
   - Надеюсь это можно исправить использованием Clover
     - Попробовал в Clover 5150 на основе [этого EFI](https://github.com/Andrej-Antipov/X99-K9-Machinist-Hackintosh/blob/main/Clover-5150-Ventura-X99K9-iEngeneer.zip) - проблема с запуском Windows после macOS Monterey повторилась
10. При создании отчета в AIDA64 (последняя версия 6.85.6300 Extreme) система полностью зависает на этапе "Debug - PCI", который отображается в левом нижнем углу окна. Поэтому отчет из AIDA64 сделать мне не получилось
    - Естественно перед этим она зависала на этапе сканирования датчиков, но отключение пункта Строка состояния -> HWMon Modules -> PCH / Bibxy, позволила продвинуться дальше датчиков

## Интересные страницы

- https://www.tonymacx86.com/threads/the-perfect-customac-pro-x99-a-ii-i7-6950x-128gb-g-skill-tridentz-aorus-gtx-1080-ti-xtreme.211621/
- https://github.com/KGP/X99-System-SSDTs
- https://github.com/Andrej-Antipov/X99-K9-Machinist-Hackintosh
- https://www.youtube.com/watch?v=3p3SG4FXmZo
- https://github.com/gsantos022/efi-machinist-x99-rs9-xeon-e2673-v3-rx570
- https://github.com/luchina-gabriel/EFI-HUANANZHI-X99-QD4-2630L-RX5500XT