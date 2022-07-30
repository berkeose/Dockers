# Docker
### Docker; açık kaynak kodlu verimlilik aracıdır. Yazılım geliştirme ve dağıtım sürecinde farklılık yaratan bir metot olarak kabul görür.
### Docker bu farkı “konteynerler” aracılığı ile gerçekleştirir. Konteynerler, uygulama kodlarını ve bunların bağlılıklarını içeren yazılım birimleridir. 
### Yazılımı bulunduğu ortamdan izole ederek, geliştirildiği işletim sisteminden bağımsız olarak çalıştırılabilmesini sağlar.

## Container : 
### Sanal makinelere (VM’ler) benzer bir rol oynayan bir uygulama dağıtım teknolojisidir. Tıpkı geleneksel sanallaştırma gibi, container’lar da uygulamalarınız için yalıtılmış ortamlar sağlar. Ancak, altyapı kaynaklarını bölmek için farklı bir yöntem kullanır.

## Docker engine: 
### Docker platformunun kalbidir. Linux veya Windows bir sisteme kurduğumuz server-client mimarisinde bir uygulamadır. 3 temel componenti vardır:
### Docker Deamon: Docker engine merkezidir. Containerler, volumeler gibi docker objelerini yaratmanızı ve yönetmenizi sağlar.RestAPI ile dış dünyayla görüşebilir.
### Docker Rest API: Diğer programlar docker deamon ile rest API aracılığyla konuşur ve ne yapması gerektiğini söyler.
### Docker CLI:Docker komut satırı arayüzüdür.
![Docker_Engine](https://user-images.githubusercontent.com/81867200/181816950-c038524b-3c00-41c2-9146-e53757f7e32f.png)


## Image:
### Bir uygulamanon çalışması için gereken ek kütüphane ve diğer öğelerin paketlenmiş halidir Okunabilir şablon olarak düşünebilirz.
## Container:
### Bu şablondan oluşturulmuş çalışan bir kopyadır. 

## Container vs Sanal Makine(Vm)
### Bare-Metal= Sunucu -> işletim sistemi -> app
### VM= Sunucu->Sanallaştırma katmanı-> işletim sistemi(10x)-> app1,app2.. // sistem izolasyonu
### Container = Sunucu-> işletim sistemi(1x) // uygulama izolasyonu
![virtual-machine-vs-container](https://user-images.githubusercontent.com/81867200/181816507-f70310bd-fd80-4935-8c22-4c2b5fff75e9.jpg)

### Notlar:
### detach container= arka planda çalışan container // docker container run -d
### çalışan container silinmez ilk stop edilmesi gerekir. -f ile zorlayarak silinebilir.
### çalışan containera docker container exec komutu ile bağlanabiliriz 
### prune komutu bütün containlerlari kapatır.
### --help ile komutları nasil kullanacağımızı görebiliriz.

## Container Temelleri
### Her container imajında, o imajdan bir container yarattığımız zaman varsayılan olarak çalışması için ayarlanmış bir uygulama vardır. 
### Bu uygulama çalıştığı sürece container ayakta kalır uygulama çalışmazsa containerda kapanır.
### Aynı imajdan 2 farklı container yaratırsak bu containerlar biribirinden bağımsız 2 farklı sistemdir.

### -Containerlar tek bir uygulama çalıştırmak için oluşturulur.
### -Containerlar tek bir uygulamanın çalışması için gerekli olan  tüm gereksinimlerin önceden hazırlandığı image dediğimiz objeden yaratılırlar.
### Containerlarla ilgili tüm gereksinimlerin imaj seviyesinde tamamlanmış olması beklenir.
### -Bir container içinde çalışan ana uygulama durdurulduğu anda container da durdurulur.Container durduğu anda sistemin bir sorun olduğunu anlayarak
### aynı imajdan aynı ayarlarla yeni bir container yaratarak sistemin çalışmaya devam etmesi sağlanabilir.
### -Container içerisinde bir uygulamada bir sıkınıtı oluşursa bu container içine bağlanarak çözülmez. Container durdurulup yeni bir container yaratılır

### // container ls -a komutu ile bütün containerlari görebiliriz.
### // docker containler logs -ID- komutu ile containerin loglarını görebiliriz.

## Union File system:
### Image sadece okunabilir katmanlardır(R/O layers) imagei çektiğimizde container yazilabilir bir katman atar (R/W Layer)
### Böylece her containerin kendine ait yazilabilir bir katmanı olur.Tüm değişiklikler orada tutulur.

## Docker Volume(container dışı bilgi saklama)
### Volume container dışında tutulur,tekrar ulaşılabilir.Bir volume ü birden fazla containera bağlayabiliriz.
### docker volume create -name- komutu ile volume yaratabiliriz.
### docker container run -it -v -name-:/uygulama alpine sh (hangi klasöer bağlamak istersek o klasörün adını yazıyoruz)(volume adı:container içindeki klasör)
### mininot: #cd ile istediğimiz klasörün içine gireibliyoruz, touch komutu ile o klasörde yeni bir dosya yaratabiliryoruz.

## Bind Mounts
### Host üstündeki bir klassörü container içine map edebiliriz. Buna Bind Mount denilir.
### C:/katman1/katman2/katman3:/usr/share/nginx/html nginx ile web sunucusunda kendi hostumuzdaki klasörü bind edebiliriz.Volume yerine kendi bilgisayrımızdaki klasörü kullanabiliyoruz.

## -ALIŞTIRMA-

### 1:Öncelikle sistemdeki tüm container,image ve volumleri görelim bunun için ayrı ayrı listeleme komutları girelim ve ardından temizlik yapmak adına makinenizdeki tüm containerları,imageları ve volumleri temizleyelim.Bunun iki yöntemi var. Bakalim siz kolay olanı mı seçeceksiniz.
### listeleme için ls 
### silmek için rm veya prune

![alıştırma1ls](https://user-images.githubusercontent.com/81867200/181830166-4e6af3c2-69d8-4de3-8029-4ee291392b5b.png)

### 2:centos ,alpine, nginx, httpd:alpine, ozgurozturknet/adanzyedocker,ozgurozturknet/hello-app,ozgurozturknet/app1 isimli imajları çalıştığımız sisteme çekelim.
pull komutu ile çekebiliyoruz.
![alıştırmapullimaj](https://user-images.githubusercontent.com/81867200/181831187-b41f55bd-0e68-4cde-a141-a42c69d2f923.png)

### 3:ozgurozturknet/app1 isimli imajdan bir containler oluşturalım.
![3 soru](https://user-images.githubusercontent.com/81867200/181832523-965024e9-b51c-4adc-8b5f-03ee5eb40d89.png)

### 4:httpd:alpine isimli imajdan detached bir container yaratalım.Yarattığımız containerin ismini ve ıd'sini görelim.
ps komutu ile isim ve ıdsine ulaşabildik.
![image](https://user-images.githubusercontent.com/81867200/181858975-ccb4d29d-5c34-42c4-81cf-0086d8b5c405.png)

### 5:Yarattığımız bu container'ın loglarına bakalım
docker logs ID veya İsmim komutu ile loglarını görebiliriz.

### 6:Containeri durduralım, ardından yeniden çalıştıralım ve son olarak container'i sistemden kaldıralım.
![soru6](https://user-images.githubusercontent.com/81867200/181859570-c174b756-4270-4b07-aaec-e99544bcb963.png)

### 7:ozgurozturknet/adanzyedocker isiml imajdan websunucu adında detached ve "-p 80:80" ile portu publish edebildiği bir container yaratalım.
![soru7](https://user-images.githubusercontent.com/81867200/181859873-b813adcb-4c42-4d00-b6ac-d8b0039a6645.png)

### 8: websunucu adlı bu container'ın içerisine bağlanalım. usr/local/apache2/htdocs klasörünün altına geçelim ve echo "denemedir" >> index.html komutuyla burdaki dosya denemedir yazısını ekleyelim.Web tarayıcıya geçerek dosyaya ekleme yapabildiğimizi görmek için refresh edelim.Sonrasında containerin içerisinden exit ile çıkalım.
![soru8](https://user-images.githubusercontent.com/81867200/181860414-93ee0ae3-649a-48d2-8ec8-531d90b39f57.png)

### 9: websunucu isimli containeri çalışırken silelim.
docker container rm -f 'containerID' komutu ile çalışan containeri silebiliriz.

### 10: alpine isimli imajdan bir container yaratalım. Ama varsayılan olarak çalışması gereken uygulama yerine "ls" uygulmasının çalışmasını sağlayalım.
 docker container run alpine ls komutu ile istenen işlemi gerçekleştirebiliriz.
 
### 11: alıştırma1 isimli bir volume yaratalım.
  docker volume create alistirma1 komutu ile istenen volume yaratıldı.
  
### 12: alpine isimli imajdan "birinci" isimli bir container yaratalım. Bu container'ı interactive modda yaratalım ve bağlanalım. Aynı zamanda alıştırma1 isimli volume'ü containerın "/test" isimli folderına mount edelim. Bu folder içerisine geçelim ve "touch abc.txt" komutuyla bir dosya yaratalım sonra dosyanın içerisine yazı ekleyelim.
![soru12](https://user-images.githubusercontent.com/81867200/181861238-7f8daed7-04cb-4630-bb5d-34eb5f5e07f9.png)

### 13:alpine isimli imajdan "ikinci" isimli bir container yaratalım.Bu container'ı interactive modda yaratalım ve bağlanabilelim.Aynı zamanda alıştırma1 isimli volume'ü bu containerin "/test" isimli folder'ına mount edelim.Bu folder içerisinde "ls" komutuyla dosyaları listeleyelim ve abc.txt dosyasının olduğunu görelim "cat" ile dosyanın içeriğini kontrol edelim.
alistirma1 isimli volume önceden oluşturulduğu için ikinci containerimızdan da ulaşabildik.
![soru13](https://user-images.githubusercontent.com/81867200/181861605-e7a4db93-7c04-47f9-b9b4-2b9915eabcae.png)

### 14: alpine isimli imajdan "ucuncu" isimli bir container yaratalım.Bu container'ı interactive modda yaratalım ve bağlanabilelim. Aynı zamanda alıştırma1 isimli volume'ü bu containerin "/test" isimli folder'ına mount edelim fakat Read Only olarak mount edelim. Bu folder içerisine geçelim ve "touch abc.txt" komutuyla yeni bir dosya yaratmaya çalışalım ve yaratamadığmızı görelim.
![soru14](https://user-images.githubusercontent.com/81867200/181861902-f9961da1-fda4-496e-8ecc-add27df280a8.png)

### 15:Bilgisayarımızda bir klasör yaratalım "örneğin c:\deneme ve bu klasör içerisinde index.html adlı bir dosya yaratıp bu dosyanın içerisine bir kaç yazı ekleyelim.

### 16:ozgurozturknet/adanzyedocker isimli imajdan websunucu1 adında detached ve "-p 80:80" ile portu publish edilmiş bir container yaratalım.Bilgisayarımızda yarattığımız klasörü container'ın içerisindeki /usr/local/apache2/htdcos klasörüne mount edelim. Web browser açarak 127.0.0.1'e gidelim ve sitemizi görelim. Daha sonra bilgisayarımızda yarattığımız klasörün içerisindeki index.html dosyasını edit edelim ve yeni yazılar ekelyelim. Web sayfasını refresh ederek bunların geldiğini görelim.
(burada bir sorun oldu)
![soru16](https://user-images.githubusercontent.com/81867200/181863582-69321fc2-2764-4689-8050-5afa2123c3bf.png)











    


