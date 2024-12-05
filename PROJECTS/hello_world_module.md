## STEP 1

* Ubuntu üzerinde "hello_world_module" adında bir klasör oluşturalım. **mkdir hello_world_module**
* Daha sonra klasör içerisine girip "hello_world_module.c" adında bir .c dosyası oluşturalım. **touch hello_world_module.c**
* Aşağıda hello_world_module.c içerisinde yer alan kodumuzun fotoğrafı yer almaktadır.

![image](https://github.com/user-attachments/assets/5c2e4058-bf9f-4621-accf-505aad2485b8)

* Ardından Makefile dosyamızı oluşturalım. 

![image](https://github.com/user-attachments/assets/9b15470d-9ce9-49e2-b425-324a0ec68d9f)


* hello_world_module.ko dosyasına ulaşmak için kodumuzu derliyoruz. Bu dosyaları oluşturduktan sonra **make** komutunu çalıştırarak aşağıdaki çıktıları elde ediyoruz.

![image](https://github.com/user-attachments/assets/ab042940-0844-44d2-b108-6c423cdffd50)



## STEP 2

* Modülümüzü çekirdeğe yüklemeden önce gelin çekirdekti modüllere bir göz atalım.
* **lsmod** komutu ile çekirdeğimizde yer alan modülleri görüntüleyebiliriz.

![image](https://github.com/user-attachments/assets/c2424f51-a3a9-4572-b9ee-6d72026851cd)

* Yukarıda görüldüğü gibi çekirdekte yer alan modüller görüntülenmektedir. Şimdi oluşturmuş olduğumuz modülü insmod komutu ile çekirdeğe yükleyelim.

![image](https://github.com/user-attachments/assets/c9dc0fd9-a0d5-4810-94f2-d32f06a330b4)

* Modülümüzü çekirdeğe yükledik bunu doğrulamak için lsmod ile çekirdekte yer alan modüllere tekrar göz atalım.

![image](https://github.com/user-attachments/assets/9d143f22-17ee-49b0-8916-9bc316712109)

* Yukarıda gözüktüğü gibi hello_world_module modülümüz çekirdeğe başarıyla yüklendi. insmod komutu ile .c kodumuzda yer alan init fonksiyonunu devreye soktuk. Ardından bu fonksiyon içerisinde yer alan bilgi mesajlarını görüntülemek için dmesg komutunu çalıştıralım.

![image](https://github.com/user-attachments/assets/82239605-0a6c-4974-bdf9-adccdab0ee06)


## STEP 3

* Şimdi yüklemiş olduğumuz "hello_world_module" kernel modülü kaldıralım. Bunun için **rmmod** komutunu kullanmalıyız bu sayede kod akışı exit fonksiyonuna yönelecek, modül kernelden kaldırılacak ve dmesg komutu ile exit fonksiyonu içerisinde yer alan bilgi mesajını görüntüleyeceğiz. Çıktılar adım adım aşağıda yer almaktadır.

* **rmmod hello_world_module** veya **rmmod hello_world_module.ko** komutlarından birini çalıştırarak modülü kernelden kaldıralım. Ardından **lsmod** komutunu çalıştırarak modülün kernel kaldırıldığını doğruluyalım.

![image](https://github.com/user-attachments/assets/a98e2208-11c4-4fdc-afee-4e58da664773)

* **dmesg** komutu ile exit fonksiyonunda bulunan bilgi mesajını görüntüleyelim.

![image](https://github.com/user-attachments/assets/bb3c2e1b-e160-40c8-b347-bc04f2c134e5)


