# Hatalar
Sunucuda ya da istekte herhangi bir hata olması durumunda aşağıdaki hata kodlarından
yararlanabilirsiniz.

Kullanıcı tarafından meydana gelen hatalar `40x`, sunucu tarafında meydana gelen hatalar
`50x` durum kodu ile gönderilmektedir. 


Hata | Anlamı
---- | ------
400  | Yanlış istek -- İstek yanlış veya eksik. Bu hata genellikle sunucunun beklediği bilgiler gelmediğinde gönderilir
401  | Yetki yok -- Token yanlış veya artık geçersiz
403  | Yasaklı -- İstek sadece admin kullanıcıları için
404  | Mevcut değil -- Yaptığınız istek veya kaynak mevcut değil
429  | Çok fazla istek -- Belirli bir zamanda çok fazla istek gönderildi. Lütfen yavaşlayın
500  | Sunucu Hatası -- İstemciden bağımsız olarak sunucuda bir hata oluştu. Daha sonra tekrar deneyin
503  | Servis mevcut değil -- Kısa bir süreliğine bakım amacıyla API hizmet vermiyor.
