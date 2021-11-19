---
title: IoTegrity API Belgesi

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Slate Kullanılmıştır</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: IoTegrity API Belgesi
---

# Giriş
IoTegrity hepimizin aşina olduğu bir REST API servisidir. JWT token kullanılmamaktadır keza
JWT, implementasyon esnasında birçok zorluk çıkarmış ve aslında ihtiyacımız olan şeyin
basit bir token altyapısı olduğunu göstermiştir.

Bu belge, API servisini ve detaylarını olabildiğince açık bir şekilde açıklayarak geliştiricinin
hayatını kolaylaştırmayı amaçlamaktadır.

API Base adresi: `https://api.iotegrity.io/`

Token gerektiren her işlem `X-HTTP-TOKEN` ile sunucuya gönderilmektedir. Bu belgelemede
`$TOKEN` değişkeni tanımlanmış ve kullanılmaktadır. Token aldıktan sonra kullandığınız terminalde
`export TOKEN=....` ile tanımlamanız halinde buradaki çağrıları kopyala / yapıştır yöntemiyle
yineleyebilirsiniz.

```shell
export TOKEN=SFMyNTY.g2gDYQFuBgB......
```


# Kullanıcı İşlemleri
## Kullanıcı Kaydı
Kayıt esnasında `kullanıcı adı`, `parola` ve `e-posta` istenmektedir. Kaydın başarılı olması durumunda
e-posta adresine doğrulama kodu gönderilmekte ve hesabın etkinleştirilmesi içerisinde bulunan
linke tıklanması gerekmektedir.

Kullanıcı adı veya e-posta mevcut ise `400` hata kodu döndürülür. Kullanıcı adınızın ve parolanızın
özgün olduğundan emin olun.

```shell
http --form POST https://api.iotegrity.io/auth/register \ 
  username=eren \
  password=12344 \
  email=eren@iotegrity.io

```

## Token Alma
Token almak için `/auth/token` adresini kullanın. Aldığınız token `X-HTTP-TOKEN` ile sunucu tarafında işlenmektedir. Dolayısıyla token gerektiren herhangi bir işlemde bu HTTP başlığını kullanılmalıdır.


```shell
http --form POST https://api.iotegrity.io/auth/token \ 
  username=USER \
  password=PASSWORD
```
```json
{
    "token": "SFMyNTY.g2gDYQFuBg.....Y2EWFJjVkFope7Q"
}
```

## Profil Görüntüleme
Aldığınız token ile kendi profilinizi `/profile` adresinden görüntüleyebilirsiniz.

```shell
http GET https://api.iotegrity.io/profile "x-http-token: $TOKEN"
```
```json
{
    "result": {
        "email": "eren@iotegrity.io",
        "id": 1,
        "username": "eren"
    }
}

```


# Cihaz İşlemleri
## Cihaz Görüntüleme
Profile kayıtlı cihazlar `/devices` adresinden görüntülenebilir.

```shell
http GET https://api.iotegrity.io/devices "x-http-token: $TOKEN"
```
```json
{
    "devices": {
        "firmware": "0.0.1",
        "id": 1,
        "inserted_at": "2021-11-14T07:11:45",
        "last_keepalive": null,
        "name": "genesis",
        "updated_at": "2021-11-14T07:11:45",
        "user": {
            "email": "eren@iotegrity.io",
            "id": 1,
            "username": "eren"
        }
    }
}
```




