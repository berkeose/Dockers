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








    


