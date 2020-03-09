# intel-nuc8i7beh-hackintosh bios version 0077
The step about how to install hackintosh on nuc8i7beh 

=====Part I  Install macOS=====

# Step 1  Prepare a USB (Should support 3.0 and at least 16GB)
# Step 2 Download "macOS Mojave 10.14.6(18G87) Installer with Clover 5033.dmg" and "etcher"
https://mirrors.dtops.cc/iso/MacOS/daliansky_macos/10.14/macOS%20Mojave%2010.14.6%2818G87%29%20Installer%20with%20Clover%205033.dmg
https://www.balena.io/etcher/
# Step 3 Plug-in USB then install the dmg via "Etcher - Balena"
# Step 4 Open NUC then click "F2" button enter to bios and check follow as below settings.
1. Enable "legacy boot"
2. Boot->Boot Configuration, disable "Network Boot"
3. Power->Secondary Power Settings "Wake on LAN from S4/S5" ->"Stay Off"
4. Boot->Secure Boot disable "Secure Boot"
# Step 5 Save and reboot, click "F10" make open via USB (Note: choose have UEFI at behind) enter Clover 
# Step 6 Select "Install macOS Mojave" -> Install MacOS
1. Select language
2. Disk Utility -> Show all device -> choose internal HD/SSD
3. Click "Erase" button 
  Name: Hackintosh or Mac...etc up to you.
  Format: Mac OS Extended (Journaled)
  Scheme: GUID Partition Map
4. Start install macOS Mojave 
NOTE:
  a. There will have about 3 times reboot please click "F10" via USB (Note: choose have UEFI at behind) open
  b. If you have " Please go to https://panic.apple.com to report this panic" error message 
  --> Go to Clover -> Option -> Graphics -> enable above one and disable below one.
  c. If you have "macOS Mojave Application is corrupted" 
  --> You can change system time, open Terminal and enter "date 010100002019" make system time to 00:00 January 1, 2019
  https://tinyurl.com/vxkde97
5. Select Country
6. Select Keyboard setting
7. Skip Send message to Apple and Apple ID setting
8. Create Account and set password
9. Skip iCloud setting
10. Finish install.

=====Part II  Through HD / SSD open mac OS instead of USB=====

# Step 7 Copy EFI folder of USB to EFI folder of internal HD/SSD
1. On mac OS then open "Terminal"
2. Enter "diskutil list" (To checking the EFI folder's IDENTIFIER)
  ex  Internal HD/SSD "disk0s1"
      USB             "disk1s1"
3. Enter "sudo diskutil mount disk0s1" (To mount EFI folder of Internal HD/SSD)
4. Enter "sudo diskutil mount disk1s1" (To mount EFI folder of USB)
5. Enter "open ." (To open finder)
6. Copy EFI from USB to Internal HD/SSD
# Step 8 Remove USB and reboot

=====Part III  Fix bug about Audio and USB type C functionality  =====

# Step 9 Update EFI folder to fix audio and USB type C functionality
1. Download EFI 
https://www.tonymacx86.com/threads/guide-installing-macos-mojave-10-14-2-on-intel-nuci5beh-using-clover-uefi-updating-to-mojave-10-14-6-on-post-2.268502/#post-1881331
2. Update EFI of Internal HD/SSD

=====Part IIII  Bluetooth solution =====

# Step 10 Enable Bluetooth function on mac OS
1. Buy GBU521 IOGEAR Bluetooth 4.0 Adapter (USB)
2. Open EFI folder of Internal HD/SSD (/Volumes/EFI/EFI/Clover)
3. Open config.plist via text editor like Sublime  
4. Add below code in KextsToPatch section

```<dict>
  ```<key>Comment</key>
  ```<string>disable port limit in XHCI kext (credit DalianSky,Ricky)</string>
  ```<key>MatchOS</key>
  ```<string>10.14.1,10.14.2</string>
  ```<key>Name</key>
  ```<string>com.apple.driver.usb.AppleUSBXHCI</string>
  ```<key>Find</key>
  ```<data>g/sPD4OPBAAA</data>
  ```<key>Replace</key>
  ```<data>g/sPkJCQkJCQ</data>
```</dict>
5. Shutdown NUC and plug in the Bluetooth adapter (USB).
6. Click "F2" button to enter bios.
7. Devices > Onboard Devices > Bluetooth (disable).
8. Save and reboot.

Refer to 
https://blog.daliansky.net/macOS-Mojave-10.14.6-18G87-Release-version-with-Clover-5033-original-image.html
https://www.jianshu.com/p/d52551119b35
https://www.tonymacx86.com/threads/guide-installing-macos-mojave-10-14-2-on-intel-nuci5beh-using-clover-uefi-updating-to-mojave-10-14-6-on-post-2.268502/#post-1881331
https://www.tonymacx86.com/threads/guide-intel-nuc7-nuc8-using-clover-uefi-nuc7i7bxx-nuc8i7bxx-etc.261711/page-48#post-1888955
https://magiclen.org/macos-installer-broken/
