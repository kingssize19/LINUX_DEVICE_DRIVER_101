## İlk Linux Aygıt Sürücüsü (First Linux Device Driver)

**Modül Bilgileri**
* License
* Author
* Module Description
* Module Version

Bu bilgiler, Linux'un module.h başlık dosyasında makrolar olarak tanımlanmıştır.

## Lisans

GPL veya GNU Genel Kamu Lisansı, yazılım için bir açık kaynak lisansıdır. Yazılımınız GPL şartlarına göre lisanslanmışsa, bu yazılım özgürdür. Ancak burada "özgür" (free) kelimesi, yazılımın tamamen ücretsiz olduğu anlamına gelmez—ücretli de olabilir. Bunun yerine, GPL'deki "özgür", özgürlük (freedom) anlamına gelir. GPL'yi destekleyenlerin ifade ettiği gibi: "Bira gibi ücretsiz değil, özgürlük gibi ücretsiz."

### Aşağıdaki lisans kimlikleri, özgür yazılım modülleri olarak kabul edilmektedir.

* "GPL": GNU Kamu Lisansı v2 veya sonrası
* "GPL v2": GNU Kamu Lisansı v2
* "GPL ve ek haklar": GNU Kamu Lisansı v2 ve ek haklar
* "Dual BSD/GPL": BSD veya GNU Kamu Lisansı v2 arasında seçim
* "Dual MIT/GPL": MIT veya GNU Kamu Lisansı v2 arasında seçim
* "Dual MPL/GPL": Mozilla Kamu Lisansı veya GNU Kamu Lisansı v2 arasında seçim

* "Proprietary": Özgür olmayan ürünler

Bazı bileşenler çift lisanslı olabilir, ancak Linux ile çalışırken GPL geçerli olduğundan bu bir sorun teşkil etmez. Benzer şekilde, LGPL (Daha Az Genel Kamu Lisansı) ile GPL birleştirildiğinde, bu bir GPL birleşik çalışmasıdır.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. **modinfo** aracı, sistemlerinin özgür yazılım olduğunu doğrulamak isteyen kullanıcılara lisans bilgilerini gösterebilir.
2. Topluluk, özgür olmayan modülleri içeren hata raporlarını göz ardı edebilir.
3. Satıcılar, kendi politikalarına dayanarak benzer şekilde hareket edebilir.

Linux aygıt sürücümüz (modül) için lisansı şu şekilde belirtebiliriz. Bunun için **Linux/module.h** başlık dosyasını eklememiz gerekir.

```c
MODULE_LICENSE("GPL");
MODULE_LICENSE("GPL v2");
MODULE_LICENSE("Dual BSD/GPL");
```
**NOT :** Bu kesinlikle zorunlu değildir, ancak modülünüzün hangi lisansa tabi olduğunu belirtmeniz iyi bir uygulamadır.


## Yazar

Bu makroyu kullanarak, bu Linux aygıt sürücüsünü veya modülünü kimin yazdığını belirtebiliriz. Böylece modinfo, kullanıcılara yazarın adını gösterebilir. Yazar bilgilerini aşağıdaki gibi belirtebilirsiniz. Bunun için Linux/module.h başlık dosyasını eklemeniz gerekir:

```c
MODULE_AUTHOR("Yazar");
```
**NOT :** "İsim <email>" veya sadece "İsim" formatını kullanabilirsiniz. Birden fazla yazar için birden fazla MODULE_AUTHOR() satırı kullanabilirsiniz.

## Modül Açıklaması

Bu makroyu kullanarak, modülün veya Linux aygıt sürücüsünün açıklamasını verebiliriz. Böylece modinfo, modül açıklamasını kullanıcılara gösterebilir. Açıklamayı şu şekilde belirtebilirsiniz:

```c
MODULE_DESCRIPTION("Bir örnek sürücü");
```

## Modül Sürümü

Bu makroyu kullanarak modülün veya sürücünün sürümünü belirtebiliriz. Böylece modinfo, modül sürümünü kullanıcılara gösterebilir.

* **Sürüm Formatı :**
  * [\<epoch>:\]<version>[\-<extra-version>\]
  * **<epoch> :** Küçük bir pozitif tamsayıdır ve sürümleri yeniden başlatmanıza olanak tanır. Eğer belirtilmezse, değeri sıfırdır. Örneğin, "2:1.0" "1:2.0" sonrası gelir.
  * **<version> :** Alfanümerik karakterler ve . içerebilir. Nümerik kısımlar sayısal sıralamayla ASCII kısımlar ise ASCII sıralamayla düzenlenir.
  * **<extraversion> :** Yerel özelleştirmeler için kullanılır, örneğin "rh3" veya "rusty1"

```c
MODULE_VERSION("2:1.0");
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Basit Çekirdek Modülü Programlama 

* Herhangi bir programlama dilinde kod yazmaya nereden başlarsınız? Genellikle bir başlangıç noktası ve bitiş noktası vardır.
* Eğer C dilini düşünürsek, başlangıç noktası main fonksiyonudur. Program, main'den başlar, diğer çağrılan fonksiyonlara geçer ve sonunda main kapanışında sonlanır.
* Linux çekirdek modülleri için durum biraz farklıdır. Burada iki ayrı fonksiyon kullanılır
 * Init Fonksiyonu
 * Exit Fonksiyonu


### Init Fonksiyonu

Bu fonksiyon, Linux aygıt sürücüsü çekirdeğe yüklendiğinde ilk olarak çalıştırılır. Örneğin, sürücüyü insmod komutuyla yüklediğimizde bu fonksiyon çalışır. 
```c
static int __init hello_world_init(void) /* Constructor */
{
    return 0;
}
module_init(hello_world_init);
```
Bu fonksiyon, kendisini module_init() makrosu ile kaydetmelidir.


### Exit Fonksiyonu

Bu fonksiyon, Linux aygıt sürücüsü çekirdekten çıkarıldığında son olarak çalıştırılır. Örneğin, sürücüyü rmmod komutuyla çıkardığımızda bu fonksiyon çalışır.
```c
void __exit hello_world_exit(void)
{

}
module_exit(hello_world_exit);
```
Bu fonksiyon, kendisini module_exit() makrosu ile kaydetmelidir. 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## printk()

C programlamada bir değer veya mesaj yazdırmak için genellikle printf() fonksiyonunu kullanırız. Ancak printf(), kullanıcı alanı fonksiyonudur, bu nedenle çekirdek seviyesinde kullanılamaz. Bunun yerine çekirdek seviyesinde kullanılabilen printk() fonksiyonu geliştirilmiştir.

printk(), mesajları öncelik seviyelerine göre sınıflandırmanıza olanak tanır. Öncelik seviyeleri için aşağıdaki makrolar kullanılır :

* **KERN_EMERG :** Acil durum mesajları (genellikle çökmeden önce).
* **KERN_ALERT :** Hemen eylem gerektiren durumlar.
* **KERN_CRIT :** Donanım veya yazılım hatalarıyla ilgili kritik durumlar.
* **KERN_ERR :** Hata durumlarını bildirir.
* **KERN_WARNING :** Ciddi sorunlara yol açmayan uyarılar.
* **KERN_NOTICE :** Normal ancak dikkat edilmesi gereken durumlar.
* **KERN_INFO :** Bilgilendirme mesajları.
* **KERN_DEBUG :** Hata ayıklama mesajları.

```c
printk(KERN_INFO "First Driver'a Hoş Geldiniz");
```


### printf() ve printk() Arasındaki Fark

1. **printk() :** Çekirdek seviyesi bir fonksiyondur ve mesajları dmesg komutuyla görebilirsiniz.
2. **printf() :** Kullanıcı alanında çalışır ve çıktı konsolunda görüntülenir.

Yeni Linux çekirdeklerinde, aşağıdaki API'leri kullanabilirsiniz.
* **pr_info :** Bilgilendirme mesajı yazdırır.
* **pr_err :** Hata mesajı yazdırır.
* **pr_warn :** Uyarı mesjaı yazdırır.

```c
pr_info("Bilgilendirme mesajı\n");
pr_err("Hata mesajı\n");
```



























