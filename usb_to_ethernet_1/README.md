# 100/1000Mbps USB 3.0 Wired USB TypeC To Rj45 Lan Ethernet Adapter RTL8153 Network Card for PC Macbook Windows Laptop

![image](../.github/images/adapter_1/full.png)

Bought on Aliexpress here: [https://www.aliexpress.us/item/3256806941075115.html?spm=a2g0o.order_list.order_list_main.5.39ca1802aVhvC9&gatewayAdapt=glo2usa](https://www.aliexpress.us/item/3256806941075115.html?spm=a2g0o.order_list.order_list_main.5.39ca1802aVhvC9&gatewayAdapt=glo2usa)

### Basic info

File contains an `AUTORUN.INF` file that attempts to take advantage of autorun on Windows. This has not worked since Windows 7 and needs to be manually enabled to run.

Tree of contents with the `AUTORUN.INF` file:
```
.
├── AUTORUN.INF
├── ControlI.dat
├── FW.bin
├── NX7202.ico
└── Setup_exe.bin
```

Once the file runs it runs a file called `Setup.exe`. This file contains a section named `_winzip` and is labeled as "malicious" by Malcore AI. See here: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdabcaee9eac363bf430](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdabcaee9eac363bf430). It is labeled as malicious due to behavior as it acts a lot like a malicious file would.

The file works the following way:
1. You plug in the adapter
2. Autorun tries to run (earleir versions it would run)
3. It runs an EXE that has a _winzip_ section in it
4. That exe unzips itself as a zip file and runs a .bat file called nx_install.bat
5. That bat file copies the exe file inside the zip called install.exe to nxinstall.exe
6. nxinstall.exe installs all the drivers for the usb to run the ethernet
7. nxinstall.exe deletes the original install.exe file

Tree of unzipped files:
```
.
├── install_exe.bin
├── netusbmini.inf
├── netusbmini.sys
├── netusbmini64.cat
├── netusbmini64.sys
├── netusbmini_cat.bin
├── nodata.txt
├── nxinstall_bat.txt
├── nxnetwdm.cat
├── nxnetwdm.inf
├── nxnetwdm.sys
├── nxnetwdm64.cat
└── nxnetwdm64.sys
```

### Internals

Chips:
![flash memory](../.github/images/adapter_1/flash.jpeg)
- MA P25Q4 202425 -- flash memory
  - [datasheet](https://www.alldatasheet.com/datasheet-pdf/pdf/1150759/PUYA/P25Q40H.html)


![microcontroller](../.github/images/adapter_1/microcontroller.jpeg)
- NX7202D M3S951.00 -- micro controller
  - Cannot locate a datasheet


![transistor](../.github/images/adapter_1/transistor.jpeg)
- 76299 -- transistor
  - [possible datasheets](https://www.alldatasheet.com/view.jsp?Searchword=76299&sField=3)


Full front:
![front](../.github/images/adapter_1/front.png)


Full back:
![back](../.github/images/adapter_1/back.png)

Board info:
![board](../.github/images/adapter_1/board.jpeg)
- JCX-013-7202 -- generic PCB board
  - No datasheets most likely Sanyo product

### File scans

`Setup.exe`:
- Full analysis: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bda9caee9eac363bf3d3](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bda9caee9eac363bf3d3)
- AI: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdabcaee9eac363bf430](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdabcaee9eac363bf430)
- Exif: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdaccaee9eac363bf45d](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdaccaee9eac363bf45d)
- Dynamic: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdaef4b96e162b80a6b0](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdaef4b96e162b80a6b0)
- Yara: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdaff4b96e162b80a6cf](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793bdaff4b96e162b80a6cf)

`install.exe`:
- Full analysis: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3a7da3e8886f5c6defa](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3a7da3e8886f5c6defa)
- AI: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3a9da3e8886f5c6df42](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3a9da3e8886f5c6df42)
- Exif: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3aa292fee4c5ea35548](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3aa292fee4c5ea35548)
- Dynamic: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3abda3e8886f5c6df85](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3abda3e8886f5c6df85)
- Yara: [https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3adcaee9eac363c0060](https://app.malcore.io/share/637b72e6d2815d7e836350da/6793c3adcaee9eac363c0060)

### File hashes
```
b15624d7189c1426b21dd7f3b3edda6b20bf856d88087a6b4c5aa67d3b08e31b  ./AUTORUN.INF
8e96bfbc7be083c30b36e7ac55cf3ff198f84908106089abf602b014497a31ba  ./ControlI.dat
3dbb1ea853cdf0653719ce300540878c8bee51dc5a69061dcaa9abd510c20443  ./FW.bin
dc040f1eaf8c1f3e711ce2c70c1c77f3d0bece7f10ce4e7ddabc11834b16f13f  ./NX7202.ico
10b4dd20f03ad951380cfff74d108103dd4179225afe59bf4c8099832811a2de  ./Setup/install_exe.bin
a235a76c38bb67e25d6f21ddfd065e69976efc151dd470ba9f2aea7d558f9851  ./Setup/netusbmini.inf
17b563e079a4256b420d17dfc110f714b2b039a36d364655ceb802b980b9fa3d  ./Setup/netusbmini.sys
24396c631e003f8c28c88f32625792f414ee575e7a031c3ff56719a987df177c  ./Setup/netusbmini64.cat
e0f0075db00798786a318c0d3cf56f850b5383648da22c1720ae1b026f1a5534  ./Setup/netusbmini64.sys
bb739b757447b567909384138a5d4bd06fcbdcacb47cc90553b32c10984ae331  ./Setup/netusbmini_cat.bin
2a5048935324b55861433d4fa98be1ef37eb712f9ec8173878c96615cb219cf0  ./Setup/nodata.txt
6adecd420c3aecb0c2e54ad7d632defca9263cbcd1e9558dd2ea02cadb7277e1  ./Setup/nxinstall_bat.txt
1c0d29199d752be45822994b031688bdb8215f9ad4d216ffeb66692c8410c6ee  ./Setup/nxnetwdm.cat
bbf6b83a16e30f1caf7c9990897c472e05a7507cffdfbd15c652f12a815a5765  ./Setup/nxnetwdm.inf
86454c8954e27cc58f99705dfde987c6820983d311f9ffecf19946d1f5493adc  ./Setup/nxnetwdm.sys
d04211809b1b1f4cf6965561cca6d2cd6209ca0c33bc94e755e3d17b3c8b0c76  ./Setup/nxnetwdm64.cat
90ea7032f075047bdb3b43f0b82fa9e695a1b69e29a7c7027664d7432a814ad3  ./Setup/nxnetwdm64.sys
dabd66200d76616a55757ac89fdb1b58cd236e701eb3adcc1dc3427a84f68060  ./Setup_exe.bin
```

