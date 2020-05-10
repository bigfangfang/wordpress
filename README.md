# wordpress

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
#### 第三步：
申請數字證書
```
sudo /opt/bitnami/letsencrypt/lego --tls --email="EMAIL-ADDRESS" --domains="DOMAIN" --domains="www.DOMAIN" --path="/opt/bitnami/letsencrypt" run
```
*替換 EMAIL-ADDRESS 成您自己的郵箱  替換 DOMAIN 成您的域名*

### 如果是 APACHE 服務器
```
sudo /opt/bitnami/bncert-tool
```
## 4 安裝wordpress主題

