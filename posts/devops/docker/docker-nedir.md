---
title: "Docker Nedir?"
subtitle: "Docker nedir? Ne işimize yarar ve avantajları nelerdir?"
date: "2024-01-11"
category: "devops"
author: "gork"
---

Yeni yılın ilk yazısından herkese merhaba! Bugün üzerine konuşacağımız mevzu **Docker** olacak. Docker serisinin ilk yazısında; docker nedir, ne işe yarar, image ve container gibi terimlere değiniyor olacağız.
İlerleyen serilerde ise bunları pratik haline getirerek devam ettiriyor olacağız.

![docker-head.png](https://raw.githubusercontent.com/gor2em/gorkdev.md/master/posts/devops/docker/images/docker-head.png?token=GHSAT0AAAAAACLHDAOZDMH4LLQJN6CF4OWGZNAKQNQ)

## Docker Nedir?

Docker açık kaynaklı bir container (kapsayıcı) teknolojisi. Docker ile aynı işletim sistemi üzerinde, birbirinden bağımsız birçok container oluşturabiliriz. Böylelikle uygulamalarımızın kolayca kurulumunu, çalışmasını ve gönderilmesini sağlayabiliriz. 

## Docker Daemon Nedir?

Hypervisor'ün dockerdaki karşılığıdır. Docker Daemon, Docker'ın arka planda çalışan servis ve sürecini yönetir. Docker, mimarisinde "client-server" modelini kullanır ve bu modelin bir parçasını oluşturur.

Temel Görevleri ise şunlardır:
- Container Yönetimi (Kullanıcı tarafından verilen komutları alır ve konteynerleri yönetir. Başlatma, durdurma ve silme gibi)
- Image İşleme (Docker Daemon, Docker Hub veya başka bir imaj kaynağından imajları çeker ve yerel imaj deposunda saklar, imajlar kullanıcı talepleri doğrultusunda işlenir)
- Container İzolasyonu
- Ağ Yönetimi
- Docker API Sunma

![containers.png](https://raw.githubusercontent.com/gor2em/gorkdev.md/master/posts/devops/docker/images/containers.jpg?token=GHSAT0AAAAAACLHDAOYPOLSBALLLCO5EQ6YZNAKSAQ)

## Docker Container Nedir?

Docker imajlarının çalışan bir örneğidir. Container teknolojisi VM gereksinimlerine ihtiyaç duymadan, farklı işletim sistemi platformlarında uygulama çalıştırmak için tasarlanmış bir tür sanallaştırma platformudur.

## Docker Image Nedir?

İçerisinde uygulamaları barındıran, container oluşturmak için kullanılan hazırlanmış paketlerdir. İmajlar paylaşılabilecek ve tekrar kullanılabilecek şekilde oluşturulur.
Örnek olarak bir image veri tabanı, işletim sistemi ya da herhangi bir dile ait olabilir. Bunlardan dilediğimizi seçip kurabilir ve yönetebiliriz.

Örneğin ben kendi bilgisayarıma postgres kurmak istiyorum. Bunun için bizlere bazı docker komutları ve docker in bilgisayarımızda kurulu olması gerekiyor.
```bash
docker pull postgres
```
diyerek postgres imajını çekerek bir container oluşturup kullanabilir ve yönetebiliriz. Uygulamalı örneklere bir sonraki yazıda daha detaylı geliyor olacağız.
 
Aşağıdaki linkte daha fazla imaj listesi mevcut.
[`images`](https://hub.docker.com/search?q=&type=image)

## Dockerfile

Yukarıdaki Image örneğinde docker pull diyerek bir imajdan container oluşturma mantığından bahsettik. Evet bunu yapabiliriz ancak bu tanımlamaları yaptığımız asıl yer `Dockerfile` adlı dosyanın ta kendisi. işte buradayız... `Dockerfile` ile ilgili uygulamamızın gereksinimlerine göre tanımlamalar yaparak imajlarımızı oluşturuyoruz.
Yine bir sonraki örneklerde, bu kısımları daha çok irdeliyor olacağız. Bir uygulama çalıştırıp ona bir Dockerfile tanımlayıp aşağıdaki işlemleri yapıyor olacağız? Aşağıdaki işlemler neler mi?

## Docker Registry

Yine bir yukarıdaki yazıda ne yaptık? `Dockerfile` denilen arkadaştan bahsettik ve dedik ki, bir imaj oluşturduk. Ee kardeşim harika nere gitti bu imaj? Uzay boşluğuna gitmeden onu yakalamamız gereken bir yer... Docker Registry. İmajların depolandığı ve paylaşıldığı yer burası.
Örnek olarak bahsedek olursak, Docker Hub. İmajlarımızı buraya gönderebilir ve onları dilediğimiz (private-public) şekilde kullanabiliriz. Bunlara ek olarak başka yerlerde de kullanmamız mümkün.

- Harbor Registry
- Azure Container Registry ACR
... gibi birçok yerde tutabiliriz.

## Docker Compose

Bir web uygulamamız olduğunu düşünelim. Bu uygulama içerisinde hem veri tabanı hem de bir servis olduğunu düşünelim. MySQL ve PHP olduğunu varsayalım. Bu artadabilir. İşte bu noktada yardımımıza Docker Compose koşuyor. Çoklu container uygulamalarımızı yönetmek için kullanırız. Birçok konteyneri bir araya getirir ve konfigürasyonunu belirtir.
`docker-compose.yml` ya da `docker-compose.yaml` şeklinde bir dosya tanımlarız ve `docker-compose up` komutuyla uygulamalarımız başlatıp çalıştırabiliriz.

## Docker Avantajları

- Hafif ve Hızlı
  Docker Containerlar, sanal makinelere göre daha hafif ve hızlıdırlar. Konteynerler, ortak bir işletim sistemi çekirdeği kullanır ve üzerine eklenen her uygulama için gerekli olan kütüphane ve dosyaları içerir. Bu nedenle, konteynerler çok hızlı şekilde başlatılabilir veyahut sonlandırılabilir.
- Taşınabilirlik
  Farklı ortamlarda local, test sunucusu vb. sorunsuz şekilde çalışmasını sağlar. 
- Kaynak Kullanımı
  Sanal makinelere göre tek bir sunucu üzerindeki kaynak tüketimi dockerda çok daha veirmlidir. Daha az kaynak ile de daha fazla container çalıştırmak mümkün.
- Ölçeklenebilirlik
  Containerların durumlarını kolaylıkla yönetebiliriz. İster yeniden başlatalım, ister silelim ya da container sayısını arttıralım. Bunun için Kubernetes bizim için altın niteliğinde. Bu teknolojiye de daha sonrasında **Kubernetes** başlığı altında değiniyor olacağız. Docker Containerlarımızı nasıl otomatik şekilde ölçeklendireceğiz onları da görüyor olacağız.


#### Docker Engine
Docker Engine, Docker'ın çekirdek bileşenidir. Docker konteynerlerini oluşturan, yöneten ve çalıştıran yazılımın temel parçasını oluşturur. DE kullanıcı tarafından verilen komutları alır, bu komutları işler ve ardından konteynerlerin oluşturulmasını, çalıştırılmasını ve yönetilmesini sağlar. Temel amacı uygulamaların hızlı bir şekilde paketlenmesini, taşınmasını ve dağıtılmasını sağlamak ve bu süreçleri standartlaştırmaktır.

#### Docker Desktop
Docker Desktop uygulaması ile platform bağımsız image, container ve daha fazlasını yönetebiliriz.

> Özetle Docker, containerları kullanarak uygulamalar oluşturmayı, dağıtmayı ve kullammayı kolaylaştıran, Linux ve Windows üzerinde çalışan açık kaynaklı bir platformdur.

Bundan sonraki docker serilerinde önce bilgisayarımız üzerinden docker komutlarını incelemek, sonrasında da **Dockerfile**, **Docker Compose** ve **Docker Registry** gibi işlemleri daha detaylı kullanıyor olacağız.

Sevgilerle.
