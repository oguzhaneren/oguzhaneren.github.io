---
title: CQRS Nedir?
description: CQRS CQS prensibinden türemiştir. Bu nedenle önce CQS'i açıklayalım.
date: 2014-09-11
tags: cqrs
layout: layouts/post.njk
---

CQRS CQS prensibinden türemiştir. Bu nedenle önce CQS'i açıklayalım.

#### [Command Query Separation](http://martinfowler.com/bliki/CommandQuerySeparation.html)

Bu prensibe göre bir nesnenin metodları Command ve Query olarak ikiye ayrılmalıdır. Bir metod bir nesne üzerinde değişiklik yaparak geriye sonuç döndürmemelidir.

- **Command** : Nesnenin durumunu değiştirir fakat geriye sonuç dönmez.
- **Query**: Sonuç döndürür fakat nesnenin durumunu değiştirmez.

Bu prensib metodların ne yaptığını, ne yapmadığını ve neyi değiştirdiğini anlamak için fayda sağlar.

#### CQRS

CQRS "Command-query responsibility segregation" anlamına gelir. Command(yazma) ve Query(okuma) olarak davranışların ayrılmasıdır.
Command ve Query farklı iki nesne tarafından ele alınırlar.

Genelde servis tanımları aşağıdaki gibidir:


``` csharp
	ProductService
		void AddProduct(productId,name)
		Product GetProduct(productId)
		void DisableProduct(productId)
		Product[] GetAllProducts(categoryId)
```

Yukarıdaki servise CQRS uygulandığında sonuçta okuma ve yazma olarak iki servis elde ederiz:

``` csharp
	ProductCommandService
		void AddProduct(productId,name)
		void DisableProduct(productId

	ProductReadService
		void AddProduct(productId,name)
		Product[] GetAllProducts(categoryId)
```

Bu yaklaşımı daha ileriye taşıyarak Command ve Query için kullanılacak veritabanlarınıda ayırabiliriz.
Bu işlem yapıldığında, okuma işlemleri için optimize edilmiş birden fazla verimodeli ve veritabanı kullanılabilir.
Okuma ve yazma veritabanlarını ayırmak CQRS ile ilişkilidir ve CQRS'in kendisi değildir, CQRS sadece okuma ve yazma işlemlerini ayırmaktır.


CQRS ilgili önemli ve ilginç olan nokta ne zaman, nerde ve nasıl kullanılacağıdır.
Bu yaklaşımı kullanmak, ölçeklenebilirlik, karmaşıklığı ve değişen iş kurallarını yönetebilmek gibi mimari sorunları daha geniş bir yelpazede çözmek için olanak sağlar.
CQRS bir mimari şablon değildir, tüm sistem düzeyinde uygulanmak yerine birden çok katılımıcının olduğu domainlerde (collaborative domain) ve ölçeklenebilirliğin önemli olduğu Bounded Context'lerde uygulanmalıdır.

Bir sonraki yazımda CQRS'in ne için uygulanması gerektiği ve hangi sorunları çözdüğünden bahsediyor olacağım.
