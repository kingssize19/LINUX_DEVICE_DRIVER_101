## Linux Aygıt Sürücüsüne Argüman Geçirme (Passing Arguments to Linux Device Driver)

Bir program içindeki diğer fonksiyonlara argüman geçirebiliriz. Ancak, bir programa argüman geçmek mümkün mü? Cevap evet. C programlamada, argc ve argv'yi ana fonksiyonun tanımına ekleyerek programa argüman geçebiliriz. Peki ya konumuza gelirsek : **Linux Aygıt Sürücüsüne argüman geçmek mümkün mü? 

## Modül Parametreleri Makroları (Module Parameters Macros)

Linux çekirdeğinde modüllere parametre geçmek için aşağıdaki makrolar kullanılır :

* module_param()
* module_param_array()
* module_param_cb()

**Parametre izinleri :**
Bir değişkenin izin türlerini almadan önce, aşağıdaki izin türlerini bilmeliyiz.

* **S_IWUSR :**
* **S_IRUSR :** Kullanıcı okuyabilir
* **S_IXUSR :** Kullanıcı çalıştırabilir
* **S_IRGRP :** Grup okuyabilir
* **S_IWGRP :** Grup yazabilir
* **S_IXGRP :** Grup çalıştırabilir

Burada S_I bir başlık niteliğindedir.

* **R :** Okuma (Read)
* **W :** Yazma (Write)
* **X :** Çalıştırma (Execute)
* **USR :** Kullanıcı (User)
* **GRP :** Grup (Group)

Bu izinleri aynı anda ayarlamak için | (veya operatörü) kullanabilirsiniz.

### module_param()

Bu makro, modül parametrelerini başlatmak için kullanılır. module_param üç parametre alır: **değişken adı**, **türü** ve **izin maskesi**. Bu makro genellikle bir dosyanın başında, herhangi bir fonksiyonun dışında tanımlanır. **module_param()** makrosu **linux/moduleparam.h**

```c
module_param(name, type, perm);
```
Bu makro, /sys/module altında bir alt dizin oluşturur. Örneğin;
```c
module_param(valueETX, int, S_IWUSR|S_IRUSR);
```
**Bu kod aşağıdaki yolu oluşturur :**
/sys/module/hello_world_module/parameters/valueETX

**Desteklenen Türler :**

* **bool :** Doğru ya da yanlış değeri (int türünde bir değişken olmalı).
* **invbool :** Boolean değerini ters çevirir (doğru -> yanlış, yanlış -> doğru).
* **charp :** Karakter işaretçisi (char pointer) türünde bir değer.
* **int, long, short, uint, ulong, ushort :** Çeşitli uzunluklarda tamsayı türleri. u ile başlayanlar işaretsiz türler içindir.


### module_param_array()

Bu makro, bir diziye argüman göndermek için kullanılır. Argümanlar, modül yükleyici tarafından virgülle ayrılmış bir liste olarak iletilir. Aşağıdaki biçimde tanımlanır :

```c
module_param_array(name, type, num, perm);
```

* **name :** Dizinin adı (ve parametrenin adı).
* **type :** Dizinin elemanlarının türü.
* **num :** Eleman sayısını tutan bir tamsayı değişkeni (isteğe bağlı, NULL olabilir).
* **perm :** İzin değeri.

### module_param_cb()

Bu makro, bir callback (geri çağırma) fonksiyonu kaydetmek için kullanılır. Argüman değiştirildiğinde, bu callback fonksiyonu çağrılır. Şimdi detaylı bir şekilde açıklayalım.

**Örnek :**
Aşağıdaki kod ile bir parametre oluşturduğumuzu varsayalım.

```c
module(valueETX, int, S_IWUSR | S_IRUSR);
```
**Bu kod aşağıdaki yolu oluşturur :**

/


















































