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
![4 soru](https://user-images.githubusercontent.com/81867200/182243618-c798af2f-6270-4b2f-a78a-99e7119615fc.png)


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

## Docker Network Driver
### Dış dünya ile konuşmayı, erieşim sağlanmasını, tüm iletişim alt yapısını docker network objeleriyle sağlarız.
### Bu objeler yaratılırken çeşitli driverlar ile yaratılır. Bu driverlar sayesinde bir networke değişik özellikler atayabiliriz. 5 temel network objesi mevcuttur.
### Bunlar :
### Bridge: Varsayılan olan driver.
### Host: Bu networke bağlı containerda network izolasyonu olmaz. Sanki o host üstünde çalışan bir process gibi hosttan ağ kaynakları kullanılır.
### MacVlan: Bu driver ileoluşturulan netowrk objeleri sayesinde containerlar fiziksel ağlara kendi mac adreslerine sahip birer fiziksel ağ adaptörüne sahipmişcesine bağlanabilirler.
### None: Hiçbir şekilde ağ bağlantısnın olmasın istersek kullanılır.
### Overlay: Ayrı hostlar üstündeki containerların aynı ağda çalışıyormuş gibi çalışmasını istediğimiz durumlarda kullanılır.

## Port Publish
### Containera dış dünyadan paket ulaşmasını sağlar
### -p veya --publish ile sistem üzerindeki portu containerdaki port ile eşleştirebiliyoruz.// docker container run -p 8080:80
### -p host_port:container_port // yani 8080'e istek geldiğinde 80 portuna gönderilicek.

## Kullanıcı Tanımlı Bridge
### Containerlar arası network izolasyonu sağlamak istersej ayrı bridge networkler yaratarak sağlayabilriz.
### Varsayılan dışında IP arakujkaru tanımlanabilir.
### Kullanıcı Tanımlı Bridge network'e bağlı containerlar birbirleriyle isimleri üzerinden haberleşebilir(Dns çözümlemesi sağlanır)
###   -aynı networke bağlı tüm containerlar birbirlerinin ismini çözebilir.

## Logging-Uygulama Günlükleri
### log, bilgisayarın gerçekleştirdiği her etkinliğin kayıt altına alınması demektir.

## STDIN-STDOUT-STDERR
### Linux sistemlerde uygulama çalıştığında bu uygulamara stdin-out-err adlı 3 genel akış aracağlığyla sağlanır.Bizimle iletişim kurmak için 3 temel giriş-çıkış noktasıdır.
### Not :docker logs -ID-   // bütün stdin-out-err leri listeler,  --details // detaylar için , -t//zaman gsöterir, --untill//o saate kadar olan logları, -- since//o saatten sonraki logları ,--tail kaç satırı görmek istediğimizi, --f//canlı olarak gözleyebilirz.

### docker top -ıd-//container processlerini gösterir.
### docker stats -ıd-// hostun üstündeki tüm containerlari gösterir ve sürekli refresh eder.

### --memory=limit
### ---memory-swap=200m -imageID-// memory dolsa bile swapdan kullanabilir.
### --cpus="coresayısı"//ne kadar cpu kullanılacağı belirlenir
### --cpuset-cpus="core nuamrası"//hangi coreları kullanacağını seçer.

## Envoirment Variable
### işletim sistemi genelinde geçerli olan değişken tanımlamaya denir.
### print env komutu ile sistemdeki envoirment variableları listeleyebilirz.
### echo $ TERM komutu ile tek envoriment variablei listeleyebilirz.
### export test="denemedir" // yeni bir envoirment variable girmemizi sağlar.
### echo $ test komutu ile yeni envoirment variableimizin içeriğini görebiliriz.

### Docker içinde envoirment variable yaratmak için:
### -- env VARIABLE = değeri veya -e VARIABLE=değeri komutlarını kullanabilirz.
### --env-file dosya_ismi komutu ile dosyamızı envoirment filein içine alabilirz.

## -ALIŞTIRMA-
### 1:İlk olarak sistemde bir temizlik yapalım ki alıştırmalarımızla bir çakışma olmasın. Varsa sistemdeki tüm containlerları ve kullanıcı tanımlı networkleri silelim.
docker ps -a ile containerlara baktık.prune ile temizledik.
docker network ls ile networklere baktık varsa docker network prune ile temizledik.

###  2:"alistirma-agi" adında ve 10.10.0.0/16 subnetinde, 10.10.10.0/24 ip-aralığından ip dağıtacak ve gateway olarak da 10.10.10.10 tanımlanacak bir kullanıcı tanımlı bridge network yaratalım.(bu sizin yerel ağınızda kullandığınız bir ağ aralığıysa başka bir cidr kullanabiliriniz).Bu ağın özelliklerini inspect komutuyla kontrol edin.
![alistirma22](https://user-images.githubusercontent.com/81867200/182049201-a9423b3d-a30b-4702-bac6-c99c9c4d71b7.png)

### 3:nginx imajının 1.16 versiyonundan web1 adından detached bir container yaratın.Bu containeri default bridge networküne degil de alistirma networküne bağlı olarak yaratın.Host'un 8080 tcp portuna gelen isteklerin bu containerın 80 portuna gitmesini sağlayın.
![alistirma23](https://user-images.githubusercontent.com/81867200/182049433-2b1c02b1-5e9a-4fff-9a37-cfd3bd81fd98.png)

### 4:Bu sisteme browser üzerinden erişin ve daha sonra bir kaç kez sayfayı refresh edin.Ardından bu container'ın loglarına erişerek az önceki erişimlerinizin loglarını kontrol edin.
127.0.0.1:8080 ile eriştik ve docker logs web1 komutu ile loglarına eriştik.

### 5:Container loglarını follow modunda takip ederken browserdan bu web sitesinde olmayan bir url'e gitmeye çalışın.Örneğin xyz.html Bunun ürettiği hatayı canlı olarak loglardan takip edin.
docker logs -f web1 ile follow modunda takip ettik ve websunucu üstünden 127.0.0.1:8080/xyz.html e gitmeye çalışıp error logunu gördük.
### 6:ozgurozturknet/adanzyedocker imajından test adından bir container yaratın.-dit ile yaratın sh shellini açın.Bu container default bridgeye bağlı olsun.
![alistirma26](https://user-images.githubusercontent.com/81867200/182049935-ad7499ef-c0e8-4a23-9643-0e3de65560e6.png)

### 7:Bu container'ı "alistirma-agi" networküne de bağlayın.
docker network connect alistirma-agi test 

### 8:Container'a attach işlemiyle bağlanın ve container içerisinden web1'i pinglemeye çalışın.Containerı kapamadan çıkın.
docker attach test daha sonra  # ping web1. Ctrl P Q ile kapatmadan çıktık
 
### 9:Bu containerların çalıştığını kontrol edin ve ardından çalışıyor haldeyken bunları silin.
docker ps ile çalıştıklarını kontrol ettik. docker container rm -f web1 test ile çalışırken sildik.

### 10:Terminalde eğitim klasörü altındaki kisim4/bolum43 klasörüne geçin.

#### 11:ozgurozturknet/webkayit imajından websrv adında detached bir container yaratın."alistirma agi" networküne bağlı olsun.Maksimum 2 logical cpu kullanacak şekilde kısıtlansın.80 portunu host üstündeki 80 portuyla publish edin. env.list dosyasını bı containera envoirment varaible olarak aktarılmasını sağlayın.
sistem belirten dosyayı bulamıyor --env-file ile ilgili sorun!
![alistirma21112](https://user-images.githubusercontent.com/81867200/182051306-08f5be97-b86b-430e-856e-c1af9a169577.png)


### 12:ozgurozturknet/webdb imajından mysqldb adında detached bir container yaratın."alistirma-agi" networküne bagli olsun.
sistem belirtiilen dosyayı bulamıyor
![alistirma21112](https://user-images.githubusercontent.com/81867200/182051306-08f5be97-b86b-430e-856e-c1af9a169577.png)


### 13:mysqldb containerının loglarını kontrol ederek düzgün bir şekilde başaltılabildiğini teyit edin.
docker logs mysqldb

### 14:Browserdan websrv containerının yayınlandığı web sitesine bağlanın.Karşınıza çıkan formu doldurup bir tane jpg dosyayı

### 15:Oluşturduğunuz containerları ve alistirma-agi ni silin.


## -IMAGE VE REGISTRY-

### Hatırlatma: Docker Image uygulamanın paketlenmiş hailidir.
### Docker imagelerine verilen isimler-tagler o imajın depolandığı yeri belirtir. docker.io/ozgurozturknet/adanzyedocker:latest
### imaj çekme işlemi için: docker image pull -ımageıd-
### Image registry:depolayıp sonradan ulaşabildiğimiz imaj depolarıdır.



## Docker Image Oluşturma(Docker File)
### Image oluşturmak için ilk olarak dockerfile oluşturmamiz gerekir.
### dockerfile: docker imagesinin kodu gibi düşünebiliriz.Kendine özgü kuralları olan bir dille yazılan ve bizlerin docker imageleri oluşturmamizi sağlayan dosyalardır.
![dockerfile](https://user-images.githubusercontent.com/81867200/182230506-7ccb0ceb-531a-4e56-a107-d968838bbaeb.png)

![dockerfile1](https://user-images.githubusercontent.com/81867200/182232515-da611c2f-facd-4bc9-9e71-a91a443a5d2e.png)



## -TALİMATLAR-

### FROM:
FROM imaj:Tag
### -Oluşturulacak imajın hangi imajdan oluşturulacağını belirten talimattır.Tek mecburi talimattır. Ör: FROM ubuntu:18:04

### RUN:   //shell de komut çalıştırız
RUN komut
### -Image oluşturulurken shell'de bir komut çalıştırmak istersek kullanılır.   Ör: RUN apt-get update

### WORKDIR:
WORKDIR klasör_lokasyonu 
### -İstediğimiz klasöre geçer ve ordan çalışmaya devam edebiliriz.

### COPY:
COPY kaynak hedef
### -Imaj içine dosya veya klasör kopyalamak için kullanırız.

### EXPOSE:
EXPOSE port
### -Bu imajdan oluşturulacak containerların hangi portlar üstünden erişebileceğini yani habgi portların yayınlanacğını bu talimatla belirtiriz.
### ÖR:EXPOSE 80/tcp

### CMD:
CMD komut
### -Bu imajdan container yaratıldığı zaman varsayılan olarak çalıştırılmasını istediğimiz komutu belirtiriz.
### ÖR:CMD java merhaba

### HEALTHCHECK:
HEALTHCHECK komut
### -Dockera bir konteynırın hala çalış çalışmadığını kontrol etmesini söyleyebiliriz.Docker ilk proccesse bakar fakat düzgün çalışıyormu diye bakmaz.HELATHCHECK buna bakabilir. Ör:HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/|| exit 1

![dockerfilekurmaadımları](https://user-images.githubusercontent.com/81867200/182242805-013ed398-c368-4acd-90b9-a9f0f3d0c2ce.png)

->> #cd c:/deneme adlı klasörün içine girdik ve code . ile vscode a bağlanıp add file ile Dockerfile oluşturduk.
![dockerfilekurmaadımları1](https://user-images.githubusercontent.com/81867200/182242975-c79cde2c-6dc3-498c-96a1-90821b6ff23d.png)

docker image build -t ozgurozturknet/merhaba .      komutu ile imajımızı oluşturduk.  "."  build context anlamında kullanılır.
 docker image history// imajın geçmişini gösterir.(katmanlı yapıyı daha iyi anlayabiliriz)
 
 ## NOTLAR:
 ### echo  // girdiğimiz komutu çıktı olarak verir.
 ### echo $ SHELL> deneme.txt   // çıktıyı hedef dosyaya gönderir.
 ### ./test.sh &  // scripti arka planda çalıştırır ve konsolda işlem yapmaya izin verir.
 ### cat abc.txt | grep 3  // soldaki komutun çıktısını sağa girdi olarak gönderir.
 ### ;  // tek satir içinde birden fazla komut girmeye izin verir.
 ### && ->   komut1&&komut2 sol olumluysa sağı çalıştır.
 ### || -> biri çalışırsa diğerini çalıştırma.
 ## dockerfile farkli bir isim ile yaratılırsa docker image -t -f .\Dockerfile.Centos .    gibi istediğimiz dockerfilein ismini belirtmemiz gerekir.
 
 ## COPY VE ADD FARKI
 ### ADD,COPY ile aynı işi yapar yani dosya yada klasör kopyalarsınız. ADD dosya kaynağında bir url olmasına da izin verir.Ayrıca ADD ile kaynak olarak bir .tar dosyası belirtilirse bu dosya imaja .tar olarak sıkıştırılmış haliyle değil de açılarak kopyalanır.
 ### Ör: ADD https://wordpress.org/latest.tar.gz/temp
 
 
 ## ENTRYPOINT VE CMD FARKI
 ## -ENTRYPOINT run time da değiştirilmez.
 ## -Aynı anda çalıştırılırlarsa ENTRYPOINT çalışır.CMD parametre olarak eklenir.
 
 ## Exec ve Shell Form Farkı
 ### Exec Form: CMD ["java","uygulama"]
 ### Shell Form: CMD java uygulama
 
 ### -Shell formunda komut girilirse container yaratıldığı zaman bu komutu shelli çalıştırarak onun içine girer
 ### -Exec oalrak girilirse komut shelli çalıştırmaz. Process oalrak çalışır.
 ### -Exec formunda shell processi çalışmadığı için ENVOIRMENT VARIABLE gibi bazı değerlere erişliemez.
 ### ENTRYPOINT ve CMD birlikte kullanılırsa EXEC FORM kullanılmalıdır.Shell formunda CMD'deki komutlar ENTRYPOINT'e parametre olarak aktarılmaz.
 
 ## Multi-Stage Build
 ### Imaj yaratma aşamasını kademelere bölmemize ve ilk kademede oluşturduğumuz imaj içerisindeki dosyaları bir sonraki kademede oluşturduğumuz imaja kopyalamaya imkan sağlar.Bu sayede nihai imaj boyutumuzun küçülmesine imkan sağlar.
 
 ![multistagebuild](https://user-images.githubusercontent.com/81867200/182481516-5a68840c-9a11-4ecb-923a-ac1a6a6e1187.png)

## BUİLD ARG
## Imajın içindeki dockerfile içerisinde değişken kullanmak istersek ARG talimatıyla tanımlayarak daha sonra değişken oalrak kullanabiliriz.Sadece imaj yaratma aşamasında geçerli olur.Imaji build ederken(docker image build -t ex --build-arg DEGISKEN=1.2.3) ile değişkenimizi atayabiliriz.

### Örnek kullanım:
 iki farklı versinoumuzu ARG VERSION olarak tanımlayarak değiştirebiliriz.
![buildarg1](https://user-images.githubusercontent.com/81867200/182486024-98a34df1-b0fd-4952-a9bb-56ea4c78450d.png)

![buildarg2 1](https://user-images.githubusercontent.com/81867200/182486312-e2def3d3-30fb-4a7a-b666-6b35ac8d0f8b.png)


![buildarg3](https://user-images.githubusercontent.com/81867200/182486060-4b6f605a-2594-45d9-8caa-6b35ba3c5157.png)

![buildarg4](https://user-images.githubusercontent.com/81867200/182486086-7cb3985e-7cca-4d8c-b1f4-0087075f7a30.png)



## -ALIŞTIRMA-

### 1:İlk olarak sistemde bir temizlik yapalım ki alıştırmalarımızla çakışma olmasın.Varsa containerları silelim.
docker container prune
### 2:Docker logout ve docker login komutlarını kullanarak hesabımızdan logout olup tekrar login olalim.
docker logout,docker login
### 3:Önceden oluşturduğumuz ve saklmamız gereken imajlar var ise bunları docker hub'a gönderin ve ardından tüm imajları silin.
![alistirma3 3](https://user-images.githubusercontent.com/81867200/182502021-443a2426-c0f7-47b7-bcc2-1fed62401a02.png)
docker image prune

### 4:Docker hub'da kendi hesabınıza ait "alistirma" adıyla public bir repository yaratın.

### 5:Centos imajının latest ve 7, ubuntu imajının latest, 18.04 ve 20.04, alpine imajının latest, nginx imajının latest ve alpine tagli imajlarını sisteme çekin.
docker pull centos:latest , docker pull centos:7, docker pull ubuntu:latest , docker pull ubuntu:18.04, docker pull ubuntu:20.04, docker pull alpine:latest,docker pull nginx:latest,docker pull nginx:alpine 
### 6:ubuntu:18.04 imajına dockerhubkullaniciadiniz/alistirma:ubuntu olarak tag ekleyin ve ardından bu yeni imaji docker hub'a gönderin.Alistirma repositorynizden imajı check edin.
docker image tag ubuntu:18.04 berkeose/alistirma:ubuntu
docker image push berkeose/alistirma:ubuntu

### 7:Bu alistirma.txt dostasının olduğu klasörde bir Dockerfile oluşturun:
### -Base imaj olarak nginx
![alistirma3 7 1 1](https://user-images.githubusercontent.com/81867200/182503302-23952905-cc00-45c7-b830-d3684ed4b14b.png)

### -İmaja LABEL="kendi adınız ve erişim bilgileriniz" şeklinde label ekleyin.
### -KULLANICI adında bir ENVOIRMENT VARIABLE tanımlayın ve değer olarak adınızı atayın
### -RENK adından bir build ARG tanımlayın
### -Sistemi update edin ve ardından curl,htop ve wget uygulamarını kurun
### -/gecici klasörüne geçin ve https://wordpress.org/latest.tar.gz dosyasını buraya ekleyin
### -/usr/share/nginx/html klasörüne geçin ve html/${RENK} klasörünün içeriğini buraya kopyalayın
### -Healthcheck talimati girelim .curl ile localhost'u kontrol etsin.Başlangıç periodu 5 saniye,deneme aralığı 30s ve zaman aşım süresi de 30 saniye olsun.Deneme sayısı 3 olsun
### -Bu imajdan bir container yaratıldığı zaman ./script.sh dosyasının çalışmasını sağlayın talimatı exec formunda girin.
![alistirma3 7a](https://user-images.githubusercontent.com/81867200/182504376-578d15df-45c6-4e10-8694-913b4ced1b5b.png)


### 8:Bu dockerfile dosyasından 2 imaj yaratın.Birinci imajda build ARG olarak RENK:kirimizi ikinci imajda da build ARG olarak RENK:sari kullanın.Kırmızı olan imajın tagi dockerhubkullaniciadiniz/alistirma:kirmizi 
docker image build -t berkeose/alistirma:sari --build-arg RENK=sari .
### sari olan imajın tagi dockerhubkullaniciadiniz/alistirma:sari olsun

### 9:dockerhub/kullaniciadiniz/alistirma:kirmizi imajını kullanarak bir container yaratın.Detach olsun makinenin 80 portuna gelen istekler bu containerın 80 portuna gitsin.Container adi kirmizi olsun.Browser'dan http://127.0.0.1 sayfasına gidip check edin.
 docker container run -d -p 80:80 --name kirmizi berkeose/alistirma:kirmizi

### 10:dockerhub/kullaniciadiniz/alistirma:sari imajını kullanarak bir container yaratın.Detach olsun makinenin 8080 portuna gelen istekler bu containerın 80 portuna gitsin. KULLANICI envoirment variable değerini "Deneme" olarak atayın.Container adı sarı olsun.Browser'dan http://127.0.0.1:8080 sayfasına gidip check edin.
docker container run -d -p 8080:80 --name sari --env KULLANICI="deneme" berkeose/alistirma:sari 
### 11:Bu containerları silelim.
docker container rm -f kirmizi sari

### 12:Bu alistirma.txt dosyasının olduğu klasörde Dockerfile.multi isimli bir Dockerfile oluşturun:
### -Bu multi-stage build alistirmasi olacak.
### -Birinci stage'i mcr.microsoft.com/java/jdk:8-zulu-alpine imajından oluşturun ve stage adı birinci olsun
### -/usr/src/uygulama klasörüne geçin ve source klasörünün içeriğini buraya kopyalayalin
### -"javac uygulama.java" komutunu çalıştırarak uygulamanızı derleyin.
### - mcr.microsoft.com/java/jre:8-zulu-alpine imajından ikinci aşamayı başlatın
### -/uygulama klasörüne geçin ve birinci aşamadaki imajın /usr/src/uygulama klasörünün içeriğini buraya kopyalayın
### -Bu imajdan container yaratıldığı zaman "java uygulama" komutnu çalıştırması için talimat girin
![alistirma3 12 1](https://user-images.githubusercontent.com/81867200/182512807-bc6da938-f216-4c3e-a6ba-12e316e964bb.png)

### 13: Bu Dockerfile.multi dosyasından dockerhub/kullaniciadiniz/alistirma:java tagli bir imaj yaratın
docker image build -t berkeose/alistirma:java -f Dockerfile.multi .
### 14:Bu imajdan bir container yaratın ve java uygulamanızın çıkardığı mesajı görün
docker run berkeose/alistirma:java
### 15:dockerhub/kullaniciadiniz/alistirma:kirmizi,dockerhub/kullaniciadiniz/alistirma:sari,dockerhub/kullaniciadiniz/alistirma:java imajlarını docker hub'a yollayın.
docker push berkeose/alistirma:kirmizi
### 16:Docker hubdaki registry isiml imajdan lokal bir Docker Registry çalıştırın.
docker run -d -p 5000:5000 --restart always --name registry registry
### 17::dockerhub/kullaniciadiniz/alistirma:kirmizi,dockerhub/kullaniciadiniz/alistirma:sari,dockerhub/kullaniciadiniz/alistirma:java imajlarını yeniden tagleyerek bu lokal registry'e gönderin ve ardından bu registry'i web arayüzünden kontrol edin.
docker image tag berkeose/alistirma:kirmizi 127.0.0.1:5000/kirmizi1:latest
docker push 127.0.0.1:5000/kirmizi1:latest
![alistirma3 16s](https://user-images.githubusercontent.com/81867200/182514338-c8086547-2f81-44af-b0a5-5e89d4521cf2.png)


## DOCKER COMPOSE
### Compose, çoklu docker uygulamalarını tanımlamak ve çalıştırmak için bir araçtır. Compose ile uygulamamızın hizmetlerini yapılandırmak için bir YAML dosyası kullanırız.Ardından,tek bir komutla,tüm hizmetleri yapılandırmamızdan oluşturur ve başlatırız.

### YAML : İnsanların kolayca okuyup anlayabilmelerini sağlayan veri serizilasyon dilidir.Konfigürasyon dosyaları oluşturulurken YAML dili kullanılır.

### Örnek YAML dosyası:
![yamlör](https://user-images.githubusercontent.com/81867200/182647276-a9fc71b6-2c84-4b0a-8f30-cbd5361568cf.png)


örn:
![image](https://user-images.githubusercontent.com/81867200/183105081-05cd7b30-1d05-44c9-8703-778d156a492a.png)


## DOCKER SWARM
### Docker Engine'e entegre bir container orchestration çözümüdür.Bir docker ana bilgisayar havuzunu tek bir sanal ana bilgisayara dönüştürür.

### DOCKER SWARM COMPONENTLERİ:
### SWARM MANAGER: Adı üstünde swarm küme(cluster) üzerindeki işlerin yönetilmesini gerçekleştiren node grubudur. Servislerin yönetilmesi, ölçekleme, sürekli monitör ederek cluster ortamını(cluster state) istenen seviyede tutma(desired state), servisler arası yük dağılımı(load balancing) gibi görevleri vardır.

### SWARM MANAGER'ın kuralları:


### WORKER NODE:İşlerin yürüdüğü yani containerlarımızın çalıştığı node’lara verilen isimdir. Bir swarm cluster’da hiç worker node yokken de cluster tüm işlevini yerine getirebilir fakat sadece worker node olan bir cluster olamaz. Bir worker node sonradan aşağıdaki kod ile manager yapılabilir.

![dockerswarm](https://user-images.githubusercontent.com/81867200/183111373-9b8d8d78-985d-41ca-8380-a363c476e074.png)









    


