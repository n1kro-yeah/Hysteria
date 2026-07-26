# Hysteria
cat > /root/hysteria-config.json << 'EOF'
{
  "log": {
    "loglevel": "none"
  },
  "inbounds": [
    {
      "tag": "HYSTERIA-BBR",
      "port": 443,
      "listen": "0.0.0.0",
      "protocol": "hysteria",
      "settings": {
        "clients": [],
        "version": 2
      },
      "streamSettings": {
        "network": "hysteria",
        "security": "tls",
        "finalmask": {
          "quicParams": {
            "debug": false,
            "congestion": "bbr"
          }
        },
        "tlsSettings": {
          "alpn": [
            "h3"
          ],
          "serverName": "artem.llm-api.click",
          "certificates": [
            {
              "keyFile": "/var/lib/remnawave/configs/xray/ssl/cert.key",
              "certificateFile": "/var/lib/remnawave/configs/xray/ssl/cert.pem"
            }
          ]
        },
        "hysteriaSettings": {
          "version": 2
        }
      }
    }
  ],
  "outbounds": [
    {
      "tag": "DIRECT",
      "protocol": "freedom"
    },
    {
      "tag": "BLOCK",
      "protocol": "blackhole"
    }
  ],
  "routing": {
    "rules": [
      {
        "ip": [
          "geoip:private"
        ],
        "outboundTag": "BLOCK"
      },
      {
        "domain": [
          "geosite:private"
        ],
        "outboundTag": "BLOCK"
      },
      {
        "protocol": [
          "bittorrent"
        ],
        "outboundTag": "BLOCK"
      }
    ]
  }
}
EOF
