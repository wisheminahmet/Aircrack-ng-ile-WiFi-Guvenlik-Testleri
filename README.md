
![Aircrack-ng ile WiFi Güvenlik Testleri](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQq5XAXu-hWPig2Q60dL_JqHpyZkoUEckjFFw&s)



# Aircrack-ng ile WiFi Güvenlik Testleri

# **Giriş**

​Bu raporda, Aircrack-ng ve Wireshark kullanarak kablosuz ağ şifrelerinin kırılması süreci ayrıntılı olarak ele alınacaktır. Rapor, kullanılan komutlar ve bu komutların ne işe yaradıkları ile bu sürecin nasıl gerçekleştirileceği hakkında adım adım bilgi verecektir. Amaç, kablosuz ağ güvenliği konusundaki farkındalığı artırmak ve bu tür saldırılardan korunmanın önemini vurgulamaktır.

## **Uyarı**

Bu proje, yalnızca yetkili olduğunuz ağlarda kullanılmalıdır. İzinsiz ağlara erişim yasa dışıdır ve ciddi yasal sonuçlar doğurabilir. Bu araçları kullanarak yapılan her türlü yasa dışı faaliyetten tamamen kullanıcı sorumludur.

## **1.Gerekli Araçlar ve Kurulum**

Aircrack-ng araç setini kurmak için aşağıdaki adımları takip edin:

### **Aircrack-ng Yükleme**
```
sudo apt update
sudo apt install aircrack-ng
```

### **Wireshark Yükleme**

```
sudo apt update
sudo apt-get install wireshark
```

## **2.Gereksinimler**

•Linux işletim sistemi (tercihen Kali Linux)

•Kablosuz ağ adaptörü (monitor mode destekleyen)

•Wordlist: Yaygın kullanılan Wi-Fi şifrelerinin bulunduğu bir liste. 

## **WireShark**

Wireshark, ağ trafiğini izlemek ve analiz etmek için kullanılan popüler ve güçlü bir ağ protokol analizörüdür. Ağ yöneticileri, güvenlik uzmanları ve geliştiriciler tarafından sıkça kullanılan Wireshark, ağ üzerindeki paketleri yakalayarak detaylı bir şekilde inceleme imkanı sunar. Kullanıcılar, Wireshark aracılığıyla ağ üzerindeki trafiği gerçek zamanlı olarak izleyebilir, belirli protokoller veya veri akışları hakkında detaylı bilgi edinebilir ve olası sorunları teşhis edebilirler. Wireshark, ağ iletişiminde meydana gelen hataları, güvenlik açıklarını ve performans problemlerini tespit etmek için vazgeçilmez bir araçtır. Bu özellikleri sayesinde, kablosuz ağlar üzerinde gerçekleştirilen handshake yakalama ve analiz işlemlerinde de sıkça kullanılır.

## **Aircrack-ng**

Aircrack-ng, kablosuz ağ şifrelerini kırmak ve güvenlik testleri gerçekleştirmek için kullanılan bir araç setidir. Bu araç seti, çeşitli bileşenlerden oluşur ve kablosuz ağlar üzerindeki güvenlik açıklarını test etmek için tasarlanmıştır. Aircrack-ng, WEP ve WPA/WPA2 gibi şifreleme protokollerini kırarak kablosuz ağların güvenliğini değerlendirmeye yardımcı olur. Araç setinin başlıca bileşenleri arasında, kablosuz ağ trafiğini yakalayan airodump-ng, paket enjeksiyonu yapan aireplay-ng, yakalanan verileri analiz eden aircrack-ng ve izleme modunu etkinleştiren airmon-ng bulunur. Aircrack-ng, güvenlik uzmanları ve ağ yöneticileri tarafından ağ güvenliğini test etmek, zayıf noktaları belirlemek ve kablosuz ağların koruma seviyesini artırmak amacıyla kullanılır.​

## **Kablosuz Ağ Adaptörünü Hazırlama​**

Kablosuz ağ adaptörünün izleme moduna alınması gereklidir. Bunun için sırasıyla gerekli adımlar izlenecektir.​

## **Kablosuz Ağ Adaptörünün Durumunu Kontrol Etme​**

Öncelikle, kablosuz ağ adaptörünün yapılandırmasını ve durumunu görüntülemek için ```iwconfig``` komutu kullanılır. Bu komut, kablosuz ağ adaptörünün adını, modunu, frekansını ve diğer önemli bilgilerini gösterir. Bu bilgileri kullanarak, hangi adaptörün izleme moduna alınması gerektiğini belirleyebiliriz.​

## **Ağ Arayüzlerinin IP Adreslerini Kontrol Etme**

```ip addr``` komutu, ağ arayüzlerinin IP adreslerini ve diğer detaylarını görüntülemek için kullanılır. Bu komut, ağ adaptörlerinin durumunu ve yapılandırmasını kontrol etmenize yardımcı olur. Bu adımda, hangi adaptörün izleme moduna alınacağını belirlemek için gerekli bilgileri sağlayabiliriz.​

## **Linux Dağıtım Bilgisini Kontrol Etme​**

```cat /etc/os-release``` komutu, kullanılan Linux dağıtımı hakkında bilgi verir. Bu komut, dağıtımın adını, versiyonunu ve diğer önemli bilgileri görüntüler. Özellikle, kullanılan araçların uyumluluğunu ve komutların çalışmasını etkileyebilecek dağıtım bilgilerini doğrulamak için kullanılır.​

## **Ağ Yöneticisi Süreçlerini Durdurma​**

Kablosuz ağ adaptörünün izleme moduna geçişini engelleyebilecek süreçleri durdurmak için ```sudo airmon-ng check kill``` komutu kullanılır. Bu komut, ağ yöneticisi ve NetworkManager gibi süreçleri devre dışı bırakır. Bu, izleme moduna geçişin sorunsuz olmasını sağlar ve böylece kablosuz ağ adaptörümüz, gerekli trafiği yakalayabilir.​

## **Kablosuz Ağ Adaptörünü İzleme Moduna Alma​**

Kablosuz ağ adaptörünü izleme moduna almak için ```sudo airmon-ng start wlan0``` komutu kullanılır. Bu komut, belirtilen kablosuz ağ adaptörünü (örneğin, wlan0) izleme moduna alır. İzleme modu, ağ trafiğini izlemek ve paket yakalamak için gereklidir. Bu mod, kablosuz ağ adaptörünün tüm trafik paketlerini almasına izin verir.​

## **Kablosuz Ağları Tarama​**

İzleme moduna alınmış adaptörle çevredeki kablosuz ağları ve bu ağlara bağlı istemcileri taramak için ```sudo airodump-ng wlan0mon``` komutu kullanılır. Bu komut, hedef ağı belirlemek ve ilgili bilgileri toplamak için kullanılır. Tarama sonucunda, çevredeki tüm erişim noktaları ve bu noktalara bağlı istemciler listelenir.​

## **Belirli Bir Erişim Noktasını Hedefleme​**

Belirli bir MAC adresine sahip erişim noktasını hedef alarak trafik yakalamak için ```sudo airodump-ng wlan0mon -d [MAC ADDRESS]``` komutu kullanılır. Bu komut, hedef ağı belirli MAC adresi ile filtreleyerek daha odaklı bir izleme sağlar. Böylece, sadece belirli bir erişim noktasına ait trafik yakalanır.​

## **Handshake Yakalama**

Belirli bir kanalda ve belirli bir BSSID (Erişim Noktası MAC Adresi) ile ilişkilendirilmiş trafik paketlerini yakalamak ve kaydetmek için ```sudo airodump-ng wlan0mon -w hack1 -c 2 --bssid [MAC ADDRESS]``` wlan0mon komutu kullanılır. Bu komut, belirli bir ağın trafiğini izleyip kaydederek handshake yakalamayı amaçlar. Yakalanan trafik, hack1 adıyla dosyaya kaydedilir.​

## **Deauthentication Saldırısı**

Belirtilen MAC adresine sahip erişim noktasına sürekli deauthentication (bağlantı kesme) paketleri göndermek için ```sudo aireplay-ng --deauth 0 -a [MAC ADDRESS] wlan0mon``` komutu kullanılır. Bu komut, istemcilerin yeniden bağlantı kurmasını sağlayarak handshake paketlerinin yakalanmasını kolaylaştırır. Deauthentication saldırısı, istemcilerin bağlantısını kesip yeniden bağlanmalarını sağlar.​

## **Handshake Analizi**

Yakalanan handshake verilerini analiz etmek için ```wireshark hack1-01.cap``` komutu kullanılır. Bu komut, yakalanan tüm trafiği içeren hack1-01.cap dosyasını Wireshark ile açar. Wireshark içinde EAPOL filtreli paketler incelenerek dört aşamalı handshake'in tüm mesajlarının yakalanıp yakalanmadığı kontrol edilir.​

## **Şifre Kırma**

Yakalanan handshake verilerini kullanarak şifre kırma işlemi için ```aircrack-ng hack1-01.cap -w /usr/share/wordlists/rockyou.txt``` komutu kullanılır. Bu komut, hack1-01.cap dosyasındaki handshake verilerini ve ```/usr/share/wordlists/rockyou.txt wordlist```'ini kullanarak şifreyi kırmaya çalışır. Aircrack-ng, wordlist'teki her bir şifreyi deneyerek doğru şifreyi bulur ve ekranda gösterir.​

# **Sonuç**

Bu raporda, Aircrack-ng ve Wireshark kullanarak kablosuz ağ şifrelerinin nasıl kırılacağı detaylı bir şekilde anlatılmıştır. Kablosuz ağ adaptörünün izleme moduna alınması, çevredeki ağların taranması, belirli bir ağın hedeflenmesi, handshake yakalama ve analiz etme adımları detaylandırılmıştır. Ayrıca, kullanılan komutlar ve bu komutların ne işe yaradığı adım adım açıklanmıştır. Kablosuz ağ güvenliği konusundaki farkındalığı artırmak ve bu tür saldırılardan korunmak için güçlü ve tahmin edilmesi zor şifreler kullanmanız ve düzenli olarak ağ güvenlik önlemlerini güncellemeniz tavsiye edilir.​


***TEŞEKKÜRLER***

**Hazırlayan**

*Ahmet Emin Doğanözü*
​











