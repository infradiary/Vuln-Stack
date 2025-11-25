This document for deploy my VA Management stack 

 #Workflow
1. Schedule Trigger → ทุกวัน 02:00
2. HTTP Request → ดึง latest report จาก OpenVAS API
3. XML → JSON
4. Filter → เอาเฉพาะ Severity High+Critical และ QOD >= 70
5. OpenCTI node → enrich ด้วย threat actor / exploitability
6. Zammad node → สร้าง ticket (deduplicate ด้วย externalID = CVE+IP)
7. Discord / Email node → แจ้งทีม


#Re
# ติดตั้ง Docker + Compose ก่อน
sudo apt update && sudo apt install docker.io docker-compose -y
sudo systemctl enable --now docker

# ดาวน์โหลดไฟล์ compose
curl -O https://raw.githubusercontent.com/unclebee/vuln-all-in-one/main/docker-compose.yml

# แก้ YOUR_SERVER_IP_OR_DOMAIN ในไฟล์ (หรือใช้ hosts file)
nano docker-compose.yml

# รันทั้งกอง
sudo docker-compose -f docker-compose.yml up -d

/vuln-stack/
├── greenbone/               ← ใส่ official Greenbone compose (ที่คุณส่งมาล่าสุด)
│   └── docker-compose.yml
│
├── opencti/                 ← ใส่ official OpenCTI 6.8.13+ compose (ที่คุณส่งมา)
│   ├── docker-compose.yml
│   └── .env                 ← ใส่ตัวแปรทั้งหมด
│
└── n8n/                     ← เอาไว้ automate ระหว่าง 2 ตัว
    └── docker-compose.yml


