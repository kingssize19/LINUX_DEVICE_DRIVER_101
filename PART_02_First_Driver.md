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

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
  * [\<epoch\]




































