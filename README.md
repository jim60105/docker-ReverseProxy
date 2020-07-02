# nginx reverse proxy 反向代理
Template改自: [nginx-proxy/docker-letsencrypt-nginx-proxy-companion](https://github.com/nginx-proxy/docker-letsencrypt-nginx-proxy-companion/blob/master/docs/Docker-Compose.md#two-containers-example)\
可在service up時自動申請SSL證書及建立路由

### **對每個後端service**添加以下環境變數
* VIRTUAL_HOST: 要往此service的網址
* CERT_NAME: SSL證書網域，必須和LETSENCRYPT_HOST的第一個相同
* LETSENCRYPT_HOST: SSL證書網域、別名
* LETSENCRYPT_EMAIL: 申請人email，到期日近會有通知。請正確填寫，似乎不容易變更

### 注意
* LETSENCRYPT_TEST=true \
申請測試證書。因正式申請有嚐試次數上限、申請數量上限，請在最後上線前再轉false

## 部屬
`docker-compose up -d`
