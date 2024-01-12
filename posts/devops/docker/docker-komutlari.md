---
title: "Docker Komutları?"
subtitle: "Docker komutları nelerdir?"
date: "2024-01-12"
category: "devops"
author: "gork"
---

Bir önceki [**yazımızda**](https://gork.dev/posts/docker-nedir) Docker'ın ne olduğundan, image ve container gibi kavramlarından bahsetmiştik. Bu yazıda ise dockerdaki komutlara göz atıyor olacağız. Başlamadan önce dockerın kurulu oluğunu varsayarak ilerliyorum.

- docker
  bu komut ile docker komutları hakkında bilgiler alabiliriz.

- docker **login**
  login komutu ile docker registry yani docker kayıt defterini çekebiliriz.

- docker **search**
  search komutu ile bir teknolojiye ait image aratabilir ve bunu çekebiliriz.
  **docker search postgres** bu komut ile postgres e ait imajları görüntüleyebilir ve bunları **pull** komutu ile çekebiliriz.
  ![docker-search.png](https://raw.githubusercontent.com/gor2em/gorkdev.md/master/posts/devops/docker/images/docker-search.png)

- docker **images**
  images komutuyla çektiğimiz tüm imajların listesini alabiliriz.
  ![docker-images.png](https://raw.githubusercontent.com/gor2em/gorkdev.md/master/posts/devops/docker/images/docker-images.png)

- docker **rmi** IMAGE-ID
  image silmek için bu komutu kullanıyoruz.

- docker **run** IMAGE-ID
  indirimiş olduğumuz imajları çalıştırmak için yukarıdaki şekilde çalıştırabiliriz.

- docker **run** -d -p 80:80 IMAGE-ID
  **-d:** containerın arka planda çalışmasını sağlar.
  **-p:** yönlendirilecek olan port.

- docker **ps**
  bu komutumuzla da container listesini görüntüleyebiliriz.

- docker **start** \ **stop** CONTAINER-ID
  start ya da stop diyerek container i başlatabilir veya durdurabiliriz.

- docker rm CONTAINER-ID
  bu komutumuzla da container id değerine göre ilgili container silinebilir.
  **rmi** şeklinde silmeye çalışırsak bu sefer hem container hem de **ilgili container a ait image** siliniyor olacak.
