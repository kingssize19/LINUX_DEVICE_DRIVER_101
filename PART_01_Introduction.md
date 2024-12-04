## Linux Nedir?

* Linux, 1991 yılında Linus Torvalds tarafından oluşturulan, UNIX tabanlı, ücretsiz ve açık kaynaklı bir işletim sistemidir (OS). Kullanıcılar, bilgisayarlar ve diğer cihazlar için dağıtımlar olarak bilinen kaynak kodunun değişikliklerini yapabilir ve varyasyonlar oluşturabilirler.

## Linux Mimarisi  (Linux Architecture)

* Linux esasen User Space ve Kernel Space olarak ikiye ayrılır. Bu iki bileşen, Kullanıcı alanı uygulamaları için Linux Çekirdeğine yönelik önceden tanımlanmış ve olgunlaşmış bir arayüz olan Sistem Çağrısı Arayüzü aracılığıyla etkileşimde bulunur.


### Kernel Space 

* Çekirdek alanı, çekirdeğin çalıştığı ve hizmetlerini sağladığı yerdir.

### User Space 

* Kullanıcı alanı, kullanıcı uygulamalarının çalıştığı yerdir.

## Linux Çekirdek Modülleri (Linux Kernel Modules)

* Çekirdek modülleri, talep üzerine çekirdeğe yüklenip boşaltılabilen kod parçalarıdır. Sistemi yeniden başlatmaya gerek kalmadan çekirdeğin işlevselliğini genişletirler.

* Özel kodlar, Linux çekirdeklerine iki yöntemle eklenebilir:
  * Temel yol, kodu çekirdek kaynak ağacına ekleyip çekirdeği yeniden derlemektir.
  * Bunu yapmanın daha verimli bir yolu, çekirdek çalışırken koda eklemektir. Bu işleme modül yükleme denir; burada modül, çekirdeğe eklemek istediğimiz kodu ifade eder.

* Bu kodları çalışma zamanında yüklediğimiz için ve bunlar resmi Linux çekirdeğinin bir parçası olmadığından, bunlara yüklenebilir çekirdek modülleri (LKM) denir; bu, "temel çekirdekten" farklıdır. Temel çekirdek, /boot dizininde bulunur ve makinemizi başlattığımızda her zaman yüklenir; oysa LKM'ler temel çekirdek yüklendikten sonra yüklenir.

* Yine de, bu LKM, çekirdeğimizin önemli bir parçasıdır ve işlevlerini tamamlamak için temel çekirdek ile iletişim kurar.

* Yüklenebilir çekirdek modülleri çeşitli amaçlara hizmet eder, ancak en yaygın uygulamalar şunlardır:
  * Aygıt sürücüleri (Device drivers)
  * Dosya sistemi sürücüleri (Filesystem drivers)
  * Sistem çağrıları (System calls)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 1. Linux Aygıt Sürücüleri (Linux Device Drivers)

* Bir aygıt sürücüsü belirli bir donanım parçası için tasarlanmıştır. Çekirdek, donanımın nasıl çalıştığıyla ilgili herhangi bir ayrıntıyı bilmeden bu donanım parçasıyla iletişim kurmak için bunu kullanır.

### 2. Dosya Sistemi Sürücüleri (Filesystem Drivers)

* Bir dosya sistemi sürücüsü, bir dosya sisteminin (genellikle bir disk sürücüsünün içeriği) içeriğini dosyalar ve dizinler olarak yorumlar. Disk sürücülerinde, ağ sunucularında ve diğer yöntemlerle dosyaları ve dizinleri depolamak için birçok farklı yol vardır. Her yol için bir dosya sistemi sürücüsüne ihtiyacınız vardır. Örneğin, Linux disk sürücülerinde neredeyse evrensel olarak kullanılan ext2 dosya sistemi türü için bir dosya sistemi sürücüsü vardır. MS-DOS dosya sistemi için de bir tane vardır, ayrıca NFS için de bir tane bulunmaktadır.

### 3. Sistem Çağrıları (System Calls)

* Kullanıcı alanı programları, çekirdekten hizmet almak için sistem çağrılarını kullanır. Örneğin, bir dosyayı okumak, yeni bir işlem oluşturmak ve sistemi kapatmak için sistem çağrıları vardır. Çoğu sistem çağrısı sisteme entegre ve oldukça standarttır, bu nedenle her zaman temel çekirdeğe gömülüdür.

* Ancak kendi sistem çağrınızı icat edebilir ve bunu bir LKM olarak kurabilirsiniz. Ya da Linux’un bir şeyi yapma şekline katılmamaya karar verirseniz, mevcut bir sistem çağrısını kendi LKM’nizle geçersiz kılabilirsiniz.


### Yüklenebilir Çekirdek Modüllerinin Avantajları (Advantages of Loadable Kernel Modules)

* Sahip oldukları en büyük avantajlardan biri, her yeni cihaz eklediğimizde veya eski bir cihazı yükselttiğimizde çekirdeği yeniden inşa etmemiz gerekmemesidir. Bu, zaman kazandırır ve ayrıca temel çekirdeğimizin hatasız kalmasına yardımcı olur.
* Yüklenebilir çekirdek modülleri (LKM'ler) oldukça esnektir; tek bir komut satırıyla yüklenip boşaltılabilirler. Bu, LKM'yi yalnızca ihtiyaç duyduğumuzda yükleyerek bellek tasarrufu sağlamaya yardımcı olur.

### Çekirdek Modülleri ve Kullanıcı Programları Arasındaki Farklar (Differences Between Kernel Modules and User Programs)

* **Kernel modüllerinin ayrı adres alanları vardır:** Bir modül kernel alanında çalışır. Bir uygulama kullanıcı alanında çalışır. Sistem yazılımı kullanıcı programlarından korunur. Kernel alanı ve kullanıcı alanı kendi bellek adres alanlarına sahiptir.
* **Kernel modüllerinin daha yüksek yürütme ayrıcalıkları vardır:** Kernel alanında çalışan kod, kullanıcı alanında çalışan koda göre daha fazla ayrıcalığa sahiptir.
* **Kernel modülleri sıralı olarak çalışmaz:** Bir kullanıcı programı tipik olarak sıralı olarak çalışır ve baştan sona tek bir görev gerçekleştirir. Bir kernel modülü sıralı olarak çalışmaz. Bir kernel modülü, gelecekteki talepleri karşılamak için kendini kaydeder.
* **Kernel modülleri farklı başlık dosyaları kullanır:** Kernel modülleri, kullanıcı programlarının gerektirdiğinden farklı bir başlık dosyası setine ihtiyaç duyar.


### Kernal Sürücüleri ile Kernal Modülleri Arasındaki Fark

* Bir kernel modülü, çalıştırma zamanında kernele eklenebilen derlenmiş bir kod parçasıdır; örneğin insmod veya modprobe ile.
* Bir sürücü, bazı donanım aygıtlarıyla iletişim kurmak için kernel içinde çalışan bir kod parçasıdır. Donanımı "sürer". Bilgisayarınızdaki neredeyse her donanım parçasının bir sürücüsü vardır.




























