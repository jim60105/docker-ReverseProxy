# nginx reverse proxy 反向代理

Template改自: [nginx-proxy/acme-companion](https://github.com/nginx-proxy/acme-companion/blob/main/docs/Docker-Compose.md#two-containers-example)
可在service up時自動申請SSL證書及建立路由

## 部屬設定

### .env

* 建議填入預設email
* 其餘選項需要再更動

### Compose up

`docker-compose up -d`

## 後端container設定

### 網路設定

使用External_network: proxy-tier

```docker run --network=proxy-tier -d IMAGE```

### 添加以下環境變數

| Key                 | Value                               | 說明                                                                                       |
|---------------------|-------------------------------------|------------------------------------------------------------------------------------------|
| `VIRTUAL_HOST`      | `your.domain.com`                   | 要往此service的網址                                                                        |
| `LETSENCRYPT_HOST`  | `your.domain.com,second.domain.com` | SSL證書網域、別名；半型逗號分隔，放第一個的是憑證主體                                         |
| `LETSENCRYPT_EMAIL` | `your@email.com`                    | 申請人email，到期日近會有通知；若不填入fallback使用DEFAULT_EMAIL；若也無DEFAULT_EMAIL時會報錯 |
| `LETSENCRYPT_TEST`  | `true` / `false`                    | 申請測試證書。因正式申請有嘗試次數限制、申請數量限制，請在最後上線前再轉false                 |
