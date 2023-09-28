# 使用说明

## 目的
使用cloudflare家的warp进行代理，绕开openai对IP的封锁

## 适用对象
ip被openai封禁的vps(访问chatgpt时错误码是1020）

## 前置准备
 * 一台已经安装好xray的VPS （ 如果没有安装xray，请查看 https://github.com/wulabing/Xray_onekey ）

## 运行
使用root账户运行以下代码：
```shell
bash <(wget -qO- -o- https://github.com/233boy/Xray/raw/main/install.sh)

# Add cloudflare gpg key
curl https://pkg.cloudflareclient.com/pubkey.gpg | sudo gpg --yes --dearmor --output /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ bookworm main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list
sudo apt-get update && sudo apt-get install cloudflare-warp
warp-cli register
warp-cli set-mode proxy
warp-cli connect
warp-cli enable-always-on
warp-cli set-proxy-port 40000
# 查询状态
systemctl status warp-svc.service
# 修改配置
curl -sSL https://github.com/bb33bb/warp2chatgpt/blob/master/warp2chatgpt.sh | bash
```
