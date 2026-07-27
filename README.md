mkdir -p /var/lib/remnawave/configs/xray/ssl

apt install -y socat

curl https://get.acme.sh | sh -s email=admin@llm-api.click

~/.acme.sh/acme.sh --set-default-ca --server letsencrypt

~/.acme.sh/acme.sh --issue --standalone -d hysteria.llm-api.click --keylength ec-256

~/.acme.sh/acme.sh --install-cert -d hysteria.llm-api.click --ecc --key-file /var/lib/remnawave/configs/xray/ssl/cert.key --fullchain-file /var/lib/remnawave/configs/xray/ssl/cert.pem
