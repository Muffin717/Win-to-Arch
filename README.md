# Winden-Archa: Windows'tan, Arch Linux'a Geçmek İçin Basit Bir Rehber

| 📝 **Söz** |
|--------------|
| "Özgürlükten doğan bunalımlar ne kadar büyük olursa olsun, hiçbir zaman fazla baskının sağladığı sahte güvenlikten daha tehlikeli değildir." |

## Giriş

**Winden-Archa**, benim tarafımdan; Windows 10/11 sistemlerinden Arch-Linux bazlı bir sisteme geçmek isteyen, işletim sistemine gereksiz yazılım katmadan ve aynı zamanda süreci mümkün olduğunca basit tutmak isteyen kişilere yardımcı olmak amacıyla yazılmıştır.

Bunu yapmanın en iyi yolunun ise deneyim paylaşmak olduğunu düşünüyorum. Dolayısıyla, bu rehber; bu yola çıkmış olan herhangi birine uyacak şekilde, çoğunlukla kendi deneyimime dayanarak hazırlandı.

> **⚠ DİKKAT:** Winden-Archa, GNU/Linux hakkında belli bir bilgiye sahip olan ve uçbirimi kullanmakta rahat olan kişileri hedef almakta. Bu belge her ne kadar Arch'ı kullanıcı dostu ve görsel yapmayı hedeflese de sorunları çözmek ve paketler/uygulamalar indirmek için uçbirimi kullanman gerekeceğinden lütfen geçiş yapmayı denemeden önce GNU/Linux uçbirimi hakkında yeterli araştırmayı yapmış olduğundan emin ol.
>
> Gelecekte yaşanabilecek karmaşaları önlemek için herhangi bir adımı denemeye yeltenmeden önce rehberin tamamını okumak önerilir.
>
> Bu rehberde kullanılması hedeflenen her şey **tamamen özgür ve açık-kaynak yazılımıdır.**

---

## Arch Kurulumunu Hazırlama

Arch Linux'un kendisine bünyesinde herhangi bir grafik arayüzüne sahip kurulum ekranı bulunmamaktdır, bu durum Arch'ın basit ve hafif doğasını zorluklarla uğraşmadan veya risk almadan kullanmak isteyenler için zorluklar oluşturabilir.

Bu nedenle mevcut duruma en uygun olarak **EndeavourOS** kullanılabilir. EndeavourOS Arch tabanlı bir işletim sistemidir ve Arch ile aynı prensipleri takip eder. Aynı zamanda güncel olarak Distrowatch'a göre en popüler Arch tabanlı işletim sistemidir.

Arch'ı (EndeavourOS'i) kurmak için önyüklenebilir bir bellek kullanabilirsiniz. Önerilen yöntem ise (en az **2GB önerilir**) bir USB belleği kullanmaktıp, onu EndeavourOS'i kurmak için bir önyüklenebilir belleğe çevirmektir.

Windows 10 veya 11 sistemlerinde bu işlemi gerçekleştirebilicek **Ventoy** ve **Rufus** gibi programlar bulunmaktadır. Bu rehberde ise önerilen program Rufus'tur, çünkü kendi deneyimlerince onu kullandım, fakat siz lütfen istediğiniz ve kullanmayı bildiğiniz farklı herhangi bir programı kullanmaktan çekinmeyin.

### Önyüklenebilir USB Belleği Oluşturmanın Adımları

#### 1. Rufus'u İndirin
- [Rufus'un resmi sitesini](https://rufus.ie/) ziyaret edin, ve sisteminize uygun olan sürümünü indirin.
- Standart ve taşınabilir sürümlerden istediğinizi seçebilirsiniz.

#### 2. EndeavourOS'in ISO Dosyasını İndirin
- [EndeavourOS'in resmi sitesini](https://endeavouros.com/) ziyaret edin ve listelenmiş aynalardan sisteminize uygun olan en güncel ISO dosyasını indirin.
- 3. adım için **imza dosyasını** indirmeyi göz önünde bulundurun.
- Bütün adımı hızlandırmak için coğrafi konumunuza en yakın olan aynayı tercih edebilirsiniz.

#### 3. ISO Dosyasını Doğrulayın (İsteğe bağlı fakat şiddetle tavsiye edilir)
İndirilen ISO dosyasının özgünlüğünü ve güvenirliğini doğrulamak için **GPG**'yi kullanabilirsiniz. Bu rehberde GPG'yi kullanmanın önerilen yolu ise **WSL (Linux için Windows Alt Sistemi)** aracığıyladır.

   ```powershell
   wsl --install -d Debian
   ```
3. Restart your computer once the installation is complete.

4. Check if GPG is installed by running:
   ```bash
   sudo apt install gpg
   ```
   If it is not installed, install it using the above command.
5. Follow the instructions on the EndeavourOS website to verify the ISO file using the **sha512** and **gpg** commands.
6. If the verification returns **"OK"**, proceed with the next step.

#### 4. Create a Bootable USB with Rufus
1. Plug in your **USB stick** and open **Rufus**.
2. If Rufus does not automatically detect your USB, manually select it.
   > **⚠ WARNING:** Ensure you select the correct drive, as **ALL DATA WILL BE ERASED**.
3. Under "Image Option," select the **EndeavourOS ISO** file (the signature file is no longer needed after verification).
4. Choose the appropriate partition scheme:
   - If your computer supports **UEFI**, select:
     - **GPT** as the partition scheme.
     - **UEFI (non CSM)** as the target system.
   - If your computer is **very old** and does **not** support UEFI, select:
     - **MBR** as the partition scheme.
     - **BIOS or UEFI** as the target system.
5. Leave other options as default.
6. Click **START**. When prompted, even if Rufus recommends choosing "Write in ISO Image mode", **do not** select that option yet.
   - This guide **recommends selecting "Write in DD Image mode"** to avoid future issues.

   > **⚠ WARNING:** Choosing this option may cause for you to not access the USB stick completely after writing the ISO to it, so make sure to use a USB stick **purely for the purposes of this task.**

7. Confirm the warnings about data loss and wait for the process to complete.
8. Once done, you will see a green box labeled **"READY."**
9. You have now successfully created a bootable USB drive. You may now eject it if needed.

---

## Installing Arch via EndeavourOS

- In order to install EndeavourOS to your system, insert the bootable USB drive to the device that you'd like to use Arch on while it is **not running**.

Proceed with booting up your system and constantly pressing the correct key to launch into your BIOS/UEFI interface. If you don't know what the correct key is, you can search for it in your computer's / motherboard's manifacturer's website, or you can try a few common keys like DEL, F2, F10, and ESC to see which one will work.

> **⚠ WARNING:** If you are installing GNU/Linux on a Windows system that is infected with malware, make sure you know the correct key. If you accidently boot into your infected operating system with the USB drive inserted, it may also get infected depending on the type and behavior of the malware. This guide recommends for you to ensure that your infected system can not access the network in any way and to test the correct key **before booting the system with the USB inserted**, to safely check if you can successfully boot into your BIOS/UEFI without taking any major risks.
>
> This method is generally safe for devices that only have the operating system infected and not the boot loader / BIOS/UEFI. Proceed with caution.
>
> You may ignore this warning if your system is not infected.

Once you safely boot up to your BIOS/UEFI with your bootable USB drive inserted, you can proceed by selecting the USB drive from the boot menu. If you have trouble locating it, you may need to check the sources of the manifacturer of your computer / motherboard.


EndeavourOS comes with the Calamares system installer, which is an installer with a graphical user interface.

EndeavourOS only ships with the following packages, which provide security and contribute to having a complete Arch system: Firefox, Pacman, Yay, FirewallD, Pipewire, Nvidia installer, Dracut, Power-Profiles-Daemon.

During the installation most of the options will be clearly understandable in your preferred language. 


- In the desktop environment choosing part, this guide recommends KDE Plasma, as it is a complete desktop environment with all the basic features as Windows and an app ecosystem with a similar look and feel. It is also highly customisable. However feel free to choose any other desktop environment or window manager.

> **⚠ WARNING:** During the **"Partition"** section of the installation, you will be asked to edit your drive's partitions and choose one to install the operating system on.
>
> If you prefer to dual-boot Windows with Arch, you can create a new partition while keeping your Windows partition. The minimum requirement mentioned in the official EndeavourOS website is 15 GB.
>
> However, if you prefer to completely wipe your drive (recommended for users who do not want to keep Windows on their system), you may delete all of the listed partitions, and install EndeavourOS on one of them.
>
> Please make sure to **backup any data from your system that you would like to keep** before proceeding.

You will also be presented with the choice to encrypt your disk. 

Disk encryption is an option which you can choose to completely encrypt your drive, which will lead you to enter passwords more than usual. If you want to protect your data from being accessed when your drive is stolen, you should enable this option. Especially recommended for laptop users.


When you're done with the disk partitioning, you may move on with the next steps and finish the installation.


## Booting into Arch
 
When your installation process is finished, you will be prompted to restart your system. Once you restart you should be greeted with your new Arch installation. If not, you may need to boot into your BIOS/UEFI and change the boot order priority, or check the boot menu settings.

> **NOTE:** EndeavourOS is esentially just Arch Linux with a graphical installation screen to make process simpler and a few packages pre-installed (that have been mentioned before), which you may choose to not install most of them during the installation screen. After the installation your system will be running Arch Linux. 

This guide mentions that the software that is used in this guide will be completely free and open-source.

For Nvidia users: If you would also like all of the software in your system to be free and open-source, you would want to use the open source Nouveau drivers instead of the closed-source proprietary Nvidia drivers. To achieve this, you can run `sudo nvidia-inst -n` in your preferred terminal and proceed. 

If you are not using an Nvidia graphics card and want to keep your system fully free and open-source, you may search for any packages that might be included in your system that are related to the proprietary Nvidia drivers as the latest EndeavourOS ISO releases ship with them, and remove them.

---

**Thank you for following this guide in your journey, and congratulations on your new Arch system!**
