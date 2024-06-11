## クライアントの秘密鍵

```
openssl genrsa -out client.key 2048
```

## クライアント証明書署名要求作成

```
openssl req -new -key client.key -subj "/C=jp/ST=Tokyo/O=Client/CN=*.aimerzarashi.com/emailAddress=user1@aimerzarashi.com" -out client.csr
```

## クライアント証明書作成

```
openssl x509 -req -days 3650 -in client.csr -CA ../inCA2.pem -CAkey ../inCA2.key -CAcreateserial -extfile ../san.txt -out client.pem
openssl x509 -text -noout -in client.pem
```

## クライアント証明書のインストール

```
openssl pkcs12 -export -in client.pem -inkey client.key -certfile ../inCA2.pem -out client.p12 -passin pass:P@ssw0rd -passout pass:P@ssw0rd
```
