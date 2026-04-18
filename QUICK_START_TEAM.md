# ⚡ QUICK START - HƯỚNG DẪN NHANH CHO TEAM

## 🎯 NGƯỜI 1: IoT Bridge Developer

### Setup Ban Đầu (Lần Đầu Tiên)
```bash
# 1. Fork repo (trên GitHub)
# https://github.com/hieu97499/parkingsystem_v3 → Fork

# 2. Clone fork của bạn
git clone https://github.com/YOUR_USERNAME/parkingsystem_v3.git C:\DoAn
cd C:\DoAn

# 3. Thêm upstream
git remote add upstream https://github.com/hieu97499/parkingsystem_v3.git

# 4. Chuyển sang nhánh iot-bridge
git fetch upstream
git checkout iot-bridge
git merge upstream/iot-bridge
```

### Làm Việc Hàng Ngày
```bash
# 1. Cập nhật code từ repo gốc
git fetch upstream
git merge upstream/dev

# 2. Code thay đổi
cd hardware/bridge/src
# ... edit files ...

# 3. Commit & Push
git add .
git commit -m "feat: thêm xử lý WebSocket events"
git push origin iot-bridge

# 4. Tạo Pull Request trên GitHub
# https://github.com/YOUR_USERNAME/parkingsystem_v3
# → Compare & pull request
# → base: dev, compare: iot-bridge
```

### Files Chính Của Bạn
```
hardware/bridge/
├── src/
│   ├── wsServer.js        (WebSocket server)
│   ├── controller.js      (Logic xử lý)
│   ├── aiClient.js        (Gọi AI service)
│   ├── backendClient.js   (Gọi Backend API)
│   ├── esp8266Handler.js  (Xử lý ESP8266)
│   └── config.js          (Cấu hình)
└── index.js               (Entry point)

hardware/arduino/
├── entry_gate/
│   └── entry_gate.ino
└── exit_gate/
    └── exit_gate.ino

hardware/esp8266/
└── esp8266_gate_bridge/
    └── esp8266_gate_bridge.ino
```

---

## 💳 NGƯỜI 2: Payment Module Developer

### Setup Ban Đầu
```bash
# Tương tự Người 1, nhưng chọn branch "payment"
git clone https://github.com/YOUR_USERNAME/parkingsystem_v3.git
cd C:\DoAn
git remote add upstream https://github.com/hieu97499/parkingsystem_v3.git
git fetch upstream
git checkout payment
git merge upstream/payment
```

### Làm Việc Hàng Ngày
```bash
# 1. Cập nhật
git fetch upstream && git merge upstream/dev

# 2. Code
cd BuildWeb/backend/src/routes
# ... edit payment, wallet, transactions ...

# 3. Commit & Push
git add .
git commit -m "feat: integrate Stripe payment API"
git push origin payment

# 4. Pull Request → base: dev, compare: payment
```

### Files Chính Của Bạn
```
BuildWeb/backend/src/routes/
├── payment.js             ← Endpoints thanh toán
├── wallet.js              ← Ví tiền
├── transactions.js        ← Giao dịch
└── reports.js             ← Báo cáo doanh thu (có liên quan)

BuildWeb/backend/src/
├── db.js                  ← Query DB (phải hiểu)
└── middleware/auth.js     ← JWT (cần authenticate)

WebApp/src/pages/
├── Wallet.jsx
├── MonthlyPasses.jsx
└── Notifications.jsx
```

### Endpoints Cần Implement
```
POST   /api/wallet/topup          → Nạp tiền
POST   /api/wallet/withdraw       → Rút tiền
GET    /api/transactions          → Lịch sử giao dịch
POST   /api/monthly-passes        → Mua hộ tháng
GET    /api/reports/revenue       → Báo cáo doanh thu
```

---

## 🎨 NGƯỜI 3: Admin Web Developer

### Setup Ban Đầu
```bash
git clone https://github.com/YOUR_USERNAME/parkingsystem_v3.git
cd C:\DoAn
git remote add upstream https://github.com/hieu97499/parkingsystem_v3.git
git fetch upstream
git checkout admin-web
git merge upstream/admin-web
```

### Làm Việc Hàng Ngày
```bash
# 1. Cập nhật
git fetch upstream && git merge upstream/dev

# 2. Code (chạy dev server)
cd BuildWeb/admin-web
npm install          # Lần đầu
npm run dev          # Port 3000

# 3. Edit files
# ... src/pages/*, src/components/* ...

# 4. Commit & Push
git add .
git commit -m "feat: thêm biểu đồ dashboard"
git push origin admin-web

# 5. Pull Request → base: dev, compare: admin-web
```

### Chạy Toàn Bộ Hệ Thống
```bash
# Terminal 1: AI Service
cd hardware/ai_service
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
python main.py

# Terminal 2: Hardware Bridge
cd hardware/bridge
npm install
node index.js

# Terminal 3: Backend
cd BuildWeb/backend
npm install
npm start

# Terminal 4: Admin Web (TẠI ĐÂY)
cd BuildWeb/admin-web
npm install
npm run dev

# Terminal 5: User App
cd WebApp
npm install
npm run dev
```

### Files Chính Của Bạn
```
BuildWeb/admin-web/src/
├── pages/
│   ├── Dashboard.jsx      ← KPI, biểu đồ
│   ├── Sessions.jsx       ← Quản lý phiên đỗ
│   ├── Users.jsx          ← Quản lý users
│   ├── Devices.jsx        ← Giám sát thiết bị
│   ├── EventLogs.jsx      ← Nhật ký sự kiện
│   ├── Reports.jsx        ← Báo cáo doanh thu
│   ├── Alerts.jsx         ← Cảnh báo
│   ├── Config.jsx         ← Cấu hình hệ thống
│   └── Login.jsx
├── components/
│   ├── Layout.jsx
│   ├── Sidebar.jsx
│   ├── Header.jsx
│   └── HardwareMonitor.jsx
├── store/
│   └── useStore.js        ← Zustand state
├── api/
│   ├── client.js
│   └── services.js        ← Gọi Backend API
└── App.jsx                ← Định nghĩa routes
```

### Công Cụ & Stack
- React 18 + React Router
- Zustand (state management)
- Tailwind CSS (styling)
- Socket.io-client (real-time)
- Recharts (biểu đồ)
- Vite (build tool)

### Chủ Đề Cần Implement
- Dashboard với KPI
- Quản lý sessions (filter, search, sort, paginate)
- Giám sát devices (online/offline status)
- Báo cáo doanh thu (charts, export)
- Alert system
- Real-time updates (WebSocket)

---

## 📱 OWNER: Quản Lý Repo

### Vai Trò
- ✅ Review Pull Requests
- ✅ Request changes nếu cần
- ✅ Merge vào `dev`
- ✅ Quản lý conflicts
- ✅ Release (merge `dev` → `main`)

### Lệnh Review & Merge
```bash
# Fetch PR từ fork của người khác
git fetch origin pull/1/head:pr-payment
git checkout pr-payment
# → Review code

# Merge vào dev
git checkout dev
git merge pr-payment
git push origin dev

# Hoặc merge trực tiếp trên GitHub (recommended)
# GitHub → Pull Requests → Merge pull request
```

---

## 🔑 KEY RULES (Luật Vàng)

1. **Luôn merge vào `dev`, KHÔNG bao giờ trực tiếp `main`**
   ```bash
   # ❌ SAI
   git push origin payment:main
   
   # ✅ ĐÚNG
   # → Tạo PR base:dev, compare:payment
   ```

2. **Luôn update từ upstream trước khi push**
   ```bash
   git fetch upstream
   git merge upstream/dev
   # → Giải quyết conflict nếu có
   git push origin payment
   ```

3. **Commit message phải rõ ràng**
   ```bash
   # ❌ SAI
   git commit -m "update"
   
   # ✅ ĐÚNG
   git commit -m "feat: integrate Stripe payment"
   git commit -m "fix: resolve WebSocket reconnection issue"
   ```

4. **KHÔNG commit .env, node_modules, build files**
   ```
   # .gitignore đã được tạo sẵn
   # Kiểm tra: git status (không nên thấy node_modules)
   ```

5. **PR nhỏ tốt hơn PR lớn**
   - PR < 400 lines: review nhanh
   - PR > 1000 lines: dễ bị reject

---

## 🆘 CẬN CỨU

### Commit sai, cần sửa message
```bash
git commit --amend -m "fix: message đúng"
git push origin payment -f      # CẢNH CÁO: Chỉ dùng khi chưa merge
```

### Xóa file nhầm
```bash
git restore src/file.js         # Undo trước khi add
git reset HEAD src/file.js      # Undo sau khi add
```

### Revert commit (khi đã push)
```bash
git revert HEAD~1               # Undo commit cuối cùng (an toàn)
git push origin payment
```

### Branch bị conflict
```bash
git fetch upstream
git merge upstream/dev
# → Resolve conflicts (edit file)
git add .
git commit -m "fix: resolve conflicts"
git push origin payment
```

---

## 📊 CHECKLIST TRƯỚC KHI GỬI PR

- [ ] Đã `git fetch upstream && git merge upstream/dev`?
- [ ] Tất cả tests xanh ✅?
- [ ] KHÔNG có `console.log()` debug?
- [ ] KHÔNG có `.env` trong commit?
- [ ] Commit messages rõ ràng?
- [ ] Code format đúng (dùng Prettier/ESLint)?
- [ ] README/docs updated (nếu cần)?
- [ ] Link được issue nếu fix bug?

---

## 📞 LIÊN HỆ & HỎI ĐÁPMỚI câu hỏi:
- 📝 Tạo **Issue** trên GitHub
- 💬 Chat qua Zalo / Telegram
- 🤝 Pair programming nếu cần

---

## 🚀 START NOW!

**Untuk dimulai:**

```bash
# Gửi GitHub username của bạn
# Owner sẽ add bạn làm collaborator

# Sau đó:
1. Fork repo
2. Clone fork
3. Add upstream
4. Switch branch
5. Code 💪
6. Commit & Push
7. Pull Request
8. Merge 🎉
```

Chúc bạn coding vui vẻ! 🎉

