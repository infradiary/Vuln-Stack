# Internal Vulnerability Management Stack (2025–2026)

ระบบ Vulnerability Management 100% ฟรี สำหรับ internal network  
ประกอบด้วย:
- Greenbone Community Edition (OpenVAS) → https://YOUR_IP:8081
- OpenCTI 6.8+ (Threat Intelligence) → https://YOUR_IP:8080
- n8n (Automation) → https://YOUR_IP:5678
- Zammad / Grafana (optional)

## วิธีเปิดเครื่องครั้งแรก (หลัง clone)

```bash
cd vuln-stack

# 1. Greenbone
cd greenbone && docker compose up -d

# 2. OpenCTI (รอ Greenbone พร้อมก่อน)
cd ../opencti
cp .env.example .env   # แล้วแก้ password
docker compose up -d

# 3. n8n
cd ../n8n && docker compose up -d
```

## การอัปเดต
```bash
git pull
docker compose -f greenbone/docker-compose.yml pull
docker compose -f greenbone/docker-compose.yml up -d
```
