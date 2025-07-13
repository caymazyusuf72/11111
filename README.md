#!/bin/bash

# BASİT WIREGUARD SERVER KURULUMU (Debian 12)

WG_PORT=51820
WG_INTERFACE="wg0"
WG_SERVER_IP="10.66.66.1"
WG_CLIENT_IP="10.66.66.2"
WG_NETMASK="/24"
WG_DIR="/etc/wireguard"

echo "[+] WireGuard kuruluyor..."
apt update && apt install -y wireguard qrencode

echo "[+] Anahtarlar oluşturuluyor..."
SERVER_PRIV=$(wg genkey)
SERVER_PUB=$(echo "$SERVER_PRIV" | wg pubkey)
CLIENT_PRIV=$(wg genkey)
CLIENT_PUB=$(echo "$CLIENT_PRIV" | wg pubkey)

echo "[+] Yapılandırma dosyası yazılıyor: $WG_DIR/wg0.conf"
cat > $WG_DIR/$WG_INTERFACE.conf <<EOF
[Interface]
Address = $WG_SERVER_IP$WG_NETMASK
ListenPort = $WG_PORT
PrivateKey = $SERVER_PRIV
PostUp = iptables -A FORWARD -i $WG_INTERFACE -j ACCEPT; iptables -A FORWARD -o $WG_INTERFACE -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i $WG_INTERFACE -j ACCEPT; iptables -D FORWARD -o $WG_INTERFACE -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
PublicKey = $CLIENT_PUB
AllowedIPs = $WG_CLIENT_IP/32
EOF

echo "[+] IP yönlendirme açılıyor..."
echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf
sysctl -p

echo "[+] WireGuard başlatılıyor..."
systemctl enable wg-quick@$WG_INTERFACE
systemctl start wg-quick@$WG_INTERFACE

echo "[+] Client yapılandırma:"
CLIENT_CONFIG=$(cat <<EOC
[Interface]
PrivateKey = $CLIENT_PRIV
Address = $WG_CLIENT_IP$WG_NETMASK
DNS = 1.1.1.1

[Peer]
PublicKey = $SERVER_PUB
Endpoint = $(curl -s ifconfig.me):$WG_PORT
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25
EOC
)

echo "$CLIENT_CONFIG" > ~/client.conf
echo "$CLIENT_CONFIG"

echo "[+] QR Kod (mobil cihaz için):"
qrencode -t ansiutf8 < ~/client.conf

echo "[✔] WireGuard kuruldu ve çalışıyor."
