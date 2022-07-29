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


    


