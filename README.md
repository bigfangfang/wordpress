# 如何在GCP谷歌雲上搭建 一鍵安裝wordpress、 註冊域名、申請數字證書、設置美觀的主題完整教程 附有商業主題免費下載喔！讓小白也能自己建網站！

## 1 註冊免費域名

## 2 申請免費谷歌雲 一鍵按照wordpress（bitnami公司 ）

## 3 申請網站數字證書
    
bitnami安裝數字證書說明文檔：https://docs.bitnami.com/google/how-to/generate-install-lets-encrypt-ssl/#alternative-approach

*本視頻是NGINX 服務器*

### 如果是 NGINX 服務器
#### 第一步：
Install The Lego Client
```
cd /tmp
curl -Ls https://api.github.com/repos/xenolf/lego/releases/latest | grep browser_download_url | grep linux_amd64 | cut -d '"' -f 4 | wget -i -
tar xf lego_vX.Y.Z_linux_amd64.tar.gz
sudo mkdir -p /opt/bitnami/letsencrypt
sudo mv lego /opt/bitnami/letsencrypt/lego
```


#### 第二步：
關閉所有服務
```
sudo /opt/bitnami/ctlscript.sh stop
```

申請數字證書
```
sudo /opt/bitnami/letsencrypt/lego --tls --email="EMAIL-ADDRESS" --domains="DOMAIN" --domains="www.DOMAIN" --path="/opt/bitnami/letsencrypt" run
```
*注意：替換 EMAIL-ADDRESS 成您自己的郵箱  替換 DOMAIN 成您的域名*


#### 第三步：
配置服務器使用數字證書

```
sudo mv /opt/bitnami/nginx/conf/server.crt /opt/bitnami/nginx/conf/server.crt.old
sudo mv /opt/bitnami/nginx/conf/server.key /opt/bitnami/nginx/conf/server.key.old
sudo mv /opt/bitnami/nginx/conf/server.csr /opt/bitnami/nginx/conf/server.csr.old
sudo ln -sf /opt/bitnami/letsencrypt/certificates/DOMAIN.key /opt/bitnami/nginx/conf/server.key
sudo ln -sf /opt/bitnami/letsencrypt/certificates/DOMAIN.crt /opt/bitnami/nginx/conf/server.crt
sudo chown root:root /opt/bitnami/nginx/conf/server*
sudo chmod 600 /opt/bitnami/nginx/conf/server*
```
*替換 DOMAIN 成您的域名 有兩行要替換喔  例如： DOMAIN.key 替換成 您的域名.key* 千萬要改喔！



打開所有服務
```
sudo /opt/bitnami/ctlscript.sh start
```
#### 第四步：

打開https://你的域名  看看是否有一個小鎖🔒


#### 自動更新數字證書
創建自動執行腳本
```
sudo nano /opt/bitnami/letsencrypt/scripts/renew-certificate.sh
```
複製內容
```
#!/bin/bash

sudo /opt/bitnami/ctlscript.sh stop nginx
sudo /opt/bitnami/letsencrypt/lego --tls --email="EMAIL-ADDRESS" --domains="DOMAIN" --path="/opt/bitnami/letsencrypt" renew --days 90
sudo /opt/bitnami/ctlscript.sh start nginx
```


使得腳本可以執行

```
sudo chmod +x /opt/bitnami/letsencrypt/scripts/renew-certificate.sh
```

执行以下命令以打开crontab编辑器
```
sudo crontab -e
```
将以下行添加到crontab文件并保存：
```
0 0 1 * * /opt/bitnami/letsencrypt/scripts/renew-certificate.sh 2> /dev/null
```
## 4 安裝wordpress主題

商業主題網站https://themeforest.net/
innovation主題：https://themeforest.net/item/innovation-multiconcept-news-magazine-blog-theme/14672414
innovation主題 大方下載地址：

ranbron主題：https://sites.bolvo.com/ranbron-theme/?storefront=envato-elements
ranbron主題 大方下載地址：

本教程YouTube視頻版本請移步：



