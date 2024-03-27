---
title: "RabbitMQ Deduplication"
subtitle: "RabbitMQ Deduplication Kullanımı"
date: "2024-03-27"
category: "be"
author: "gork"
---

RabbitMQ ile deduplication işlemini nasıl yapabiliriz? Bugün onu irdeleyelim. Öncelikle benim bu eklentiye neden ihtiyacım oldu? Sonsuz bir döngüde verileri kuyruklara aktarmam gerekliydi.
Buradaki sorun kuyruklara aktarılan verilerin benzersiz olması gerektiğiydi. Yani kuyruğa aktarılan veri var ise tekrar gönderilmemeliydi. İlk çözüm olarak bunları dinlemeye koyuldum ve var mı yok mu kontrolüne giriştim. Girişmemle çıkmam bir oldu çünkü bu tarz işlem oldukça mantıksızdı. Biraz araştırdıktan sonra RabbitMQ içerisine plugins yani eklenti kurabiliyormuşuz.

## Paketi içe alıyoruz

[Eklentiye buradan ulaşabilirsiniz](https://github.com/noxdafox/rabbitmq-message-deduplication)

**C:\Program Files\RabbitMQ Server\rabbitmq_server-your-version**
Kendi dizininizde ilgili paketi kurabilir ve yönetebilirsiniz.

## RabbitMQ kuyruk ekleme
Eğer her şeyi sorunsuz yaptıysak, kuyruk oluşturma anında arguments eklemeli ve headers içerisinde bu veriyi göndermeliyiz ki ayrıştırma yapılabilsin.


![rabbitmq-deduplication-arguments](https://github.com/gor2em/gorkdev.md/blob/master/posts/be/rabbitmq/images/queue.png)

**x-message-deduplication** özelliğini kuyruk özelinde true yaparak aktifleştirmiş oluyoruz.

	```headers := make(amqp.Table)
	headers["x-deduplication-header"] = id

	if err := ch.Publish(
		"",        // Exchange
		queueName, // Routing key
		false,     // Mandatory
		false,     // Immediate
		amqp.Publishing{
			Body:    messageBody,
			Headers: headers,
		},
	); err != nil {
		return err
	}
  ```

Kod örneğinde is header içerisinde bize gelen id değerini header de set ediyoruz ve bu şekilde kuyruklara aktarım sağlıyoruz.

![rabbitmq-deduplication-header](https://github.com/gor2em/gorkdev.md/blob/master/posts/be/rabbitmq/images/deduplication.png)

Sevgilerle.
