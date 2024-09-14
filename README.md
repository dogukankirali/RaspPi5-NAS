# RaspPi5-NAS
### Raspberry Pi 5 & OpenMediaVault & CasaOS - NAS Installation Guide

1. **Download the latest version of Raspberry Pi Imager**.  
   [Source: Raspberry Pi Software](https://www.raspberrypi.com/software/)

2. Once the **MicroSD card** is connected to the computer, open Raspberry Pi Imager.

3. From Raspberry Pi Imager:
   - Select the Raspberry Pi device version (5).
   - For the operating system, choose **Raspberry Pi OS (other)** and then **Raspberry Pi OS Lite (64-bit)**.  
     _(If 64-bit is not selected, some issues may arise while installing CasaOS, especially with package installation and PUBLIC_KEY retrieval.)_
   - Select the connected **MicroSD card**.
   - After clicking **Next**, under **Edit Settings**:
     - Change the hostname.
     - Set a username and password.
     - Optionally, fill in the wireless details.
     - Configure the locale settings.
     - Enable SSH.  
       _(The process may take longer depending on the write speed of the MicroSD card.)_

4. Once the process is complete, insert the **MicroSD card** into the Raspberry Pi (connected to power but not yet turned on), and power it on.  
   _(If wireless information was not entered during setup, a LAN connection for internet access will be required.)_

5. From the modem interface, under **DHCP settings**, assign a static IP to the Raspberry Pi connected to the network (it should appear with the hostname you set). This prevents the IP from changing after each reboot.

6. From a computer on the same network, open a terminal and run the command ```ssh username@raspberry-pi-ip``` to establish an SSH connection.

7. When prompted with "Are you sure you want to continue connecting (yes/no/[fingerprint])?", type **yes** and continue. Then enter the password you set for the user.

8. After logging into the device, run the command `sudo apt update && sudo apt upgrade`.  
   _(You may be asked questions during the process. Respond with Y or yes.)_

9. Then, run the command ```sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash``` to install **OpenMediaVault**.  
   _(This process may take some time.)_

10. After installation, wait for the device to reboot itself. Once rebooted, log in again via SSH.

11. Enter the IP address in a web browser to access the **OpenMediaVault** interface and log in.  
    _(Default credentials: username: admin | password: openmediavault)_  
    After logging in, change the password.

12. Under **System -> Workbench**, change the port from **80 to 8080**. Then, access the IP via IP:8080 and log in again.

13. Go to **Storage -> File Systems**, and click the "Mount" button to select the connected storage disk.  
    _(The disk format should preferably be EXT4.)_

14. Under **Services -> SMB/CIFS -> Settings**, check the **Enabled** box and save.

15. In **Storage -> Shared Folders**, create a shared folder.

16. Under **Services -> SMB/CIFS -> Shares**, check the **Enabled** box, then select the shared folder you created from the **Shared Folder** dropdown.

17. Under **Users -> Users**, select a user and click "Edit" to change the password.  
    _(This is independent of the password prompted during the first login.)_

18. In **Storage -> Shared Folders**, select the relevant folder and go to **Access Control List**. Check the **Recursive** box and save.

19. Go back to the terminal connected via SSH and run the command ```curl -fsSL https://get.casaos.io | sudo bash```.

20. Once the installation is complete, access the Raspberry Pi IP through a browser (without specifying a port). Create a user.

### The process is complete!

-----------------------

# RaspPi5-NAS
### Raspberry Pi 5 & OpenMediaVault & CasaOS - NAS Installation Guide

1. **Raspberry Pi İmaj Yöneticisi'nin** son sürümü indirilir.  
   [Kaynak: Raspberry Pi Software](https://www.raspberrypi.com/software/)

2. **MicroSD Kart** bilgisayara bağlandıktan sonra Raspberry Pi İmaj Yöneticisi açılır.

3. Raspberry Pi İmaj Yöneticisi'nden:
   - Raspberry Pi Device cihaz versiyonuna göre (5) seçilir.
   - İşletim sistemi olarak **Raspberry Pi OS (other)** altındaki **Raspberry Pi OS Lite (64-bit)** seçilir.  
     _(64-bit seçilmezse, CasaOS indirilirken bazı paketlerin ve PUBLIC_KEY'lerin çekilmesinde sorun yaşanabilir.)_
   - Takılan **MicroSD kart** seçilir.
   - **Next**'e tıkladıktan sonra **Edit Settings** altından:
     - Hostname değiştirilir.
     - Username ve Password belirlenir.
     - İsteğe bağlı olarak wireless bilgileri doldurulur.
     - Locale ayarları yapılır.
     - SSH açılır.  
       _(Süreç MicroSD kartın yazma hızına göre değişebilir.)_

4. İşlem bittikten sonra **MicroSD kart**, güce bağlanmış ama açılmamış Raspberry Pi'a takılır ve Raspberry Pi açılır.  
   _(Eğer kurulumda wireless bilgisi girilmediyse LAN ile internet bağlantısı gerekli olacak.)_

5. Modem arayüzünden **DHCP ayarları** içerisinden, ağa bağlanmış Raspberry Pi'a (hostname ile gözükmeli) statik IP verilerek, her boot işleminden sonra IP değişmesi engellenir.

6. Aynı ağa bağlı bilgisayarınız ile bir terminal açarak, ```ssh username@raspberry-pi-ip``` komutuyla SSH bağlantısı açılır.

7. "Are you sure you want to continue connecting (yes/no/[fingerprint])?" sorusuna **yes** diyerek devam edilir. Daha sonra belirlediğiniz kullanıcı şifresi girilir.

8. Cihaza giriş yapıldıktan sonra `sudo apt update && sudo apt upgrade` komutu çalıştırılır.  
   _(İşlem sırasında sorular sorulabilir. Y veya yes şeklinde cevaplanır.)_

9. Daha sonra ```sudo wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash``` komutu ile **OpenMediaVault** kurulur. _(İşlem uzun sürebilir.)_

10. Kurulumdan sonra cihazın kendine reboot atması beklenir. Reboot'tan sonra tekrar SSH ile giriş yapılır.

11. IP adresi tarayıcı üzerinden girilerek **OpenMediaVault** arayüzü açılır ve giriş yapılır.  
    _(Default credentials: username: admin | password: openmediavault)_  
    Giriş yapıldıktan sonra şifre değiştirilir.

12. **System -> Workbench** altından port **80'den 8080**'e taşınır. IP:8080'e gidilerek tekrar giriş yapılır.

13. **Storage -> File Systems** üzerinden "Mount" tuşuna basılarak takılan depolama diski seçilir. _(Disk formatı tercihen EXT4 olmalı.)_

14. **Services -> SMB/CIFS -> Settings** altından en üstteki **Enabled** tiklenerek kaydedilir.

15. **Storage -> Shared Folders** içerisinden bir paylaşılan klasör oluşturulur.

16. **Services -> SMB/CIFS -> Shares** altından en üstteki **Enabled** tiklenir ve altındaki **Shared Folder**'dan eklenen paylaşılan klasör eklenir.

17. **Users -> Users** altından kullanıcı seçilerek "Edit" tuşuna basılır ve şifre değiştirilir.  
    _(İlk girişte sorulan şifre ile bir bağı yok.)_

18. **Storage -> Shared Folders** altından ilgili klasör seçilerek **Access Control List**'e gidilir. Orada **Recursive** tiklenerek kaydedilir.

19. Daha sonra SSH ile bağlandığınız terminale dönülerek ```curl -fsSL https://get.casaos.io | sudo bash``` komutu çalıştırılır.

20. Kurulum bittikten sonra Raspberry Pi'a verdiğiniz IP'ye tarayıcı ile gidilir (port vermeden). Kullanıcı oluşturulur.

### İşlem tamam!
