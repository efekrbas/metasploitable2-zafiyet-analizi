# metasploitable2-calismam
İlk olarak netdiscover kullanarak ağdaki cihazları keşfettim.
<img width="945" height="244" alt="image" src="https://github.com/user-attachments/assets/3d857e55-3cef-43de-9d46-b12950031c73" />

 
Sonrasında 192.168.138.129 IP’li bir cihaz buldum.
Bulduğum 192.168.138.129 IP adresine nmap taraması gerçekleştirdim.
<img width="945" height="452" alt="image" src="https://github.com/user-attachments/assets/d14fa87d-77c3-4d90-bd62-0a0a2f24bde7" />

 
Samba smbd 3.X - 4.X ve vsftpd 2.3.4 versiyonlu servisleri listede gördüm ve araştırdığımda çok kritik açıklarının olduğunu farkettim.
Samba servisinde kullanabileceğim exploiti bulmak için search parametresini kullandım ve görseldeki 3 numaralı adı exploit/multi/samba/usermap_script olan exploiti kullanabileceğimi farkettim.
<img width="945" height="216" alt="image" src="https://github.com/user-attachments/assets/14c36289-b6d2-42e8-9466-9eef5b40b96b" />


 
Sonrasında ise msfconsole aracını kullanarak exploit/multi/samba/usermap_script exploitini use parametresi ile seçtim, set RHOSTS komutu ile ilk adımda bulduğum girdim ve exploit komutunu yazıp exploti çalıştırdım. Çalıştırdığım exploitle bir shell elde ettim, elde ettiğim shellde whoami komutunu kullandığımda her hangi bir şifre gerekmeden root (en yetkili kullanıcı) olduğumu farkettim.
<img width="945" height="272" alt="image" src="https://github.com/user-attachments/assets/2d1dbf73-2e0e-4589-8cc6-608d1f7831f9" />

 

Ardından backdoor oluşturmak için unix/ftp/vsftpd_234_backdoor exploitini kullandım
<img width="945" height="262" alt="image" src="https://github.com/user-attachments/assets/c13e4653-6323-4fe5-b889-8f6e59eefa26" />

 

Hedef sistem üzerinde çalışan VNC (Virtual Network Computing) servisi, uzaktan masaüstü yönetimi sağlamak amacıyla yapılandırılmıştır. Ancak, yapılan güvenlik incelemesinde bu servisin kimlik doğrulama mekanizmasının zayıf olduğu veya varsayılan düşük güvenlikli bir parola (password) kullandığı tespit edilmiştir. Yapılan taramalarda hedef sistemin 8180 portunda çalışan Apache Tomcat servisinin yönetim panelinin varsayılan kimlik bilgileriyle (tomcat:tomcat) erişilebilir olduğu tespit edilmiştir. Metasploit üzerinden ilgili istismar modülü kullanılarak şu adımlar gerçekleştirilmiştir:
<img width="939" height="383" alt="image" src="https://github.com/user-attachments/assets/8f05af27-181e-4ed3-877f-529d4ad28482" />

Payload Yükleme: Hedef sunucuya kötü amaçlı bir Java Arşivi (.war dosyası) yüklenmiştir. (Görselde görülen jRAmlAv...war dosyası).
Tetikleme: Yüklenen bu dosya üzerinden bir .jsp betiği çalıştırılarak hedef sistemin saldırgan makineye (192.168.138.128) geri bağlantı (reverse connection) kurması sağlanmıştır.
Oturum Açılması: 2026-03-04 tarihinde, saat 05:40:42'de hedef sistem üzerinde tam yetkili bir Meterpreter oturumu başarıyla açılmıştır.
2. Elde Edilen Bilgiler (Keşif Aşaması) Başarılı sızma işlemi sonrası sysinfo komutu çalıştırılarak hedef sistem hakkında şu kritik bilgiler elde edilmiştir:
Bilgisayar Adı: metasploitable
İşletim Sistemi: Linux 2.6.24-16-server (i386 mimarisi)
Sistem Dili: en_US (İngilizce)
Meterpreter Türü: java/linux
<img width="945" height="231" alt="image" src="https://github.com/user-attachments/assets/25aadcbf-d2f0-4fc0-9b61-ce93d637bacb" />

 

UnrealIRCd 3.2.8.1 Arka Kapı İstismarı (Root Erişimi)
Port: 6667/tcp
Zafiyet: UnrealIRCd Backdoor
Erişim Seviyesi: Root (Tam Yetki)
İşlem: Hedef sistemin IRC servisinde bulunan yerleşik arka kapı, exploit/unix/irc/unreal_ircd_3281_backdoor modülüyle tetiklenmiştir.
Sonuç: Herhangi bir parola girişine gerek kalmaksızın, saldırgan makine (192.168.138.128) ile hedef (192.168.138.129) arasında bir Command Shell oturumu açılmıştır.
Kanıt: whoami komutuna karşılık alınan root çıktısı, sistem üzerinde en üst düzey yetkilerin ele geçirildiğini kanıtlamaktadır
<img width="945" height="128" alt="image" src="https://github.com/user-attachments/assets/3bbd2aa1-1dbc-4e4b-8eff-a9e311584e04" />

 

Ingreslock (Port 1524) Zayıf Yapılandırma Sömürüsü
İşlem: Herhangi bir exploit aracı kullanmadan, sadece Netcat (nc) ile 1524 portuna bağlantı isteği gönderilmiştir.
Bulgu: Sistemin hiçbir kimlik doğrulaması (kullanıcı adı/şifre) sormadan doğrudan bir root shell sunduğu görülmüştür.
Analiz: Görseldeki root@metasploitable:/# ibaresi, sistemde unutulmuş veya kasten açık bırakılmış bir yönetimsel zafiyetin varlığını kesinleştirmiştir.
<img width="545" height="144" alt="image" src="https://github.com/user-attachments/assets/3f19b4df-501a-4638-bd41-14e7b891bd0d" />
