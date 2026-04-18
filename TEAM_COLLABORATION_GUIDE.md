# 👥 HƯỚNG DẪN LÀNG VIỆC NHÓM - TEAM COLLABORATION

## 📌 Cấu Trúc Repository

```
Repository: hieu97499/parkingsystem_v3
│
├── main               (Production branch - không commit trực tiếp)
├── dev                (Development - nơi merge các feature)
├── payment            (Người 1: Xử lý thanh toán)
├── iot-bridge         (Người 2: Phần cứng IoT)
└── admin-web          (Người 3: Giao diện quản lý)
```

---

## 🎯 QUY TẮC TẠO PULL REQUEST

### Workflow Cơ Bản:

```
1. Fork repo                  (Nhân bản cá nhân)
   ↓
2. Clone fork               (Lấy về máy tính)
   ↓
3. Thêm upstream            (Kết nối với repo gốc)
   ↓
4. Tạo / Switch branch      (Chuyển sang nhánh phân công)
   ↓
5. Code & Commit            (Làm việc)
   ↓
6. Push lên fork            (Đẩy lên repo cá nhân)
   ↓
7. Tạo Pull Request         (Gửi merge request)
   ↓
8. Merge vào dev            (Owner review & merge)
```

---

## 🚀 BƯỚC 1-2: CLONE REPO (Người khác - Người 1, 2, 3)

```bash
# Bước 1: Fork repo gốc (trên GitHub)
# Vào: https://github.com/hieu97499/parkingsystem_v3
# Nhấn nút "Fork" (góc trên phải)
# → Tạo bản sao tại: https://github.com/USERNAME/parkingsystem_v3

# Bước 2: Clone repo FORK của bạn xuống máy
git clone https://github.com/YOUR_USERNAME/parkingsystem_v3.git C:\DoAn
cd C:\DoAn
```

---

## 🔗 BƯỚC 3: SETUP UPSTREAM (Quan Trọng!)

```bash
# Thêm remote "upstream" trỏ về repo gốc của chủ repo
git remote add upstream https://github.com/hieu97499/parkingsystem_v3.git

# Kiểm tra remotes
git remote -v

# Kết quả mong muốn:
# origin      https://github.com/YOUR_USERNAME/parkingsystem_v3.git (fetch)
# origin      https://github.com/YOUR_USERNAME/parkingsystem_v3.git (push)
# upstream    https://github.com/hieu97499/parkingsystem_v3.git (fetch)
# upstream    https://github.com/hieu97499/parkingsystem_v3.git (push)
```

---

## 📋 BƯỚC 4: PHÂN CÔNG NHÁNH

### Người 1 - IoT Bridge
```bash
git fetch upstream
git checkout iot-bridge
git merge upstream/iot-bridge
```

### Người 2 - Payment (Thanh toán)
```bash
git fetch upstream
git checkout payment
git merge upstream/payment
```

### Người 3 - Admin Web
```bash
git fetch upstream
git checkout admin-web
git merge upstream/admin-web
```

---

## ✏️ BƯỚC 5: LÀNG VIỆC - CODE & COMMIT

### Quy tắc Commit Message
```bash
# Format: <type>: <description>

# Types:
# feat:     Tính năng mới
# fix:      Sửa lỗi
# docs:     Cập nhật tài liệu
# style:    Format code (không thay đổi logic)
# refactor: Tái cấu trúc code
# perf:     Cải thiện performance
# test:     Thêm test

# Ví dụ:
git add .
git commit -m "feat: thêm module thanh toán"
git commit -m "fix: sửa lỗi socket.io connection"
git commit -m "docs: cập nhật README"
```

### Làm Việc Hàng Ngày
```bash
# 1. Đảm bảo branch của bạn cập nhật nhất
git fetch upstream
git merge upstream/dev       # Nếu dev có update từ owner

# 2. Code thay đổi
nano src/components/MyComponent.jsx

# 3. Commit
git add .
git commit -m "feat: hoàn thành feature X"

# 4. Push lên FORK của bạn
git push origin payment      # (Thay "payment" bằng branch của bạn)
```

---

## 📤 BƯỚC 6-7: TẠO PULL REQUEST (PR)

### Trên GitHub:

1. Vào repo FORK của bạn:
   ```
   https://github.com/YOUR_USERNAME/parkingsystem_v3
   ```

2. GitHub sẽ hiện thông báo:
   ```
   "Compare & pull request" → Nhấn nút này
   ```

3. Hoặc nhấn "Pull Requests" (tab) → "New pull request"

4. **Chọn đúng branches:**
   ```
   base repository:  hieu97499/parkingsystem_v3
   base branch:      dev             ← LUÔN MERGE VÀO DEV!
   
   head repository:  YOUR_USERNAME/parkingsystem_v3
   compare branch:   payment         ← Branch của bạn
   ```

5. **Điền tiêu đề & mô tả:**
   ```
   Title: feat: hoàn thành module thanh toán
   
   Description:
   - Thêm endpoint POST /api/transactions
   - Integrate với Stripe API
   - Thêm unit tests
   - Test trên production: ✅
   
   Closes #123 (nếu fix issue)
   ```

6. Nhấn **"Create Pull Request"**

---

## ✅ BƯỚC 8: MERGE (Người Quản Lý - Owner)

**Owner (hieu97499) sẽ:**
1. Review code
2. Request changes (nếu cần)
3. Approve
4. Merge vào `dev`
5. (Sau này merge `dev` → `main` để release)

---

## 🔄 BƯỚC 9: CẬP NHẬT KHI CÓ CODE MỚI TỪ OWNER

Khi owner merge PR của người khác vào `dev`, bạn cần update:

```bash
# 1. Fetch mới nhất từ upstream
git fetch upstream

# 2. Ở branch của bạn, merge dev mới
git checkout payment       # (Thay "payment" bằng branch của bạn)
git merge upstream/dev     # Lấy những gì vừa merge vào dev

# 3. Push lên fork của bạn
git push origin payment

# 4. Giải quyết conflict nếu có
# (Edit file → add → commit → push)
```

---

## 🚨 XUNG ĐỘT (Conflict) & CÁCH GỎI

### Khi có conflict:

```bash
git status    # Xem file nào bị conflict

# Edit file conflict, chọn phần code bạn muốn giữ lại
# Sau đó:
git add .
git commit -m "fix: resolve merge conflicts"
git push origin payment
```

File conflict sẽ có dạng:
```javascript
<<<<<<< HEAD
// Code từ branch của bạn
const x = 1;
=======
// Code từ branch khác
const x = 2;
>>>>>>> upstream/dev
```

Bạn chọn phần nào là đúng, xóa marker (`<<<<`, `====`, >>>>`)

---

## 📊 BẢNG PHÂN CÔNG

| Người | Branch | Phụ Trách | Status |
|-------|--------|----------|--------|
| Người 1 | `iot-bridge` | Hardware Bridge, ESP8266, Arduino | 🔄 Đang làm |
| Người 2 | `payment` | Module Thanh toán, Ví tiền | 🔄 Đang làm |
| Người 3 | `admin-web` | Giao diện Admin, Dashboard | 🔄 Đang làm |
| Owner | `dev`, `main` | Review, Merge, Release | ✅ Quản lý |

---

## 💾 LỆNH GIT THƯỜNG DÙNG

```bash
# Kiểm tra branch & remotes
git branch -a
git remote -v

# Cập nhật từ upstream
git fetch upstream

# Switch branch
git checkout payment
git checkout dev

# Tạo branch mới (nếu cần feature riêng)
git checkout -b feature/awesome-feature dev

# Xem thay đổi
git status
git diff

# Undo changes
git restore src/file.js        # Undo thay đổi chưa stage
git reset HEAD src/file.js     # Unstage file
git revert HEAD                # Undo commit gần nhất (an toàn)

# View commits
git log --oneline -10
git log --graph --all --decorate

# Tạo tag (để đánh dấu release)
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0
```

---

## 📋 CHECKLIST TRƯỚC KHI GỬI PR

- [ ] Đã fetch & merge `upstream/dev` mới nhất?
- [ ] Tất cả conflict đã giải quyết?
- [ ] Code đã chạy test ở local?
- [ ] Commit message rõ ràng & theo convention?
- [ ] Không có console.log debug?
- [ ] .env, node_modules, build files đã ignore?
- [ ] README hoặc docs đã update (nếu cần)?
- [ ] Code review bản thân trước khi push?

---

## 🚫 NHỮNG ĐIỀU KHÔNG NÊN LÀM

❌ **KHÔNG** commit trực tiếp vào `main` hoặc `dev`
❌ **KHÔNG** push force (`git push -f`) trên public branches
❌ **KHÔNG** để node_modules, build files, .env trong commit
❌ **KHÔNG** commit secrets, API keys, passwords
❌ **KHÔNG** rebase history của upstream branches
❌ **KHÔNG** merge lạc nhánh (ví dụ merge `payment` vào `iot-bridge`)

---

## 📞 CẢN THIỆP KHI CẬN NGẶP VẤN ĐỀ

### 1. Không thể push vì lỗi "rejected"
```bash
# Solution: Update trước khi push
git fetch origin
git merge origin/payment
git push origin payment
```

### 2. Commit sai message
```bash
# Sửa commit cuối cùng (chưa push)
git commit --amend -m "fix: message đúng"

# Nếu đã push, tạo commit sửa
git commit -m "fix: sửa typo message"
```

### 3. Xóa commit nhầm
```bash
# Xem log chi tiết
git reflog

# Checkout lại commit đó
git checkout abc123ef
```

### 4. Xóa branch nhầm
```bash
# Restore branch local
git checkout -b payment abc123ef

# Restore branch remote
git push origin payment
```

---

## 🎓 TƯ LẢM THÊM

**Sách:**
- Pro Git (miễn phí): https://git-scm.com/book/en/v2

**Công Cụ Hỗ Trợ:**
- GitHub Desktop (GUI)
- VS Code Git Extension
- GitKraken (trả phí nhưng pro)

**Best Practices:**
- Commit thường xuyên, messages rõ ràng
- Review code của nhau trước merge
- Giữ branches nhỏ & focused (1 feature per branch)
- Rebase thay vì merge khi cần history sạch

---

## 📧 LIÊN HỆ & Q&A

- 📱 Zalo / Telegram / Discord khi gặp vấn đề
- 📝 Tạo Issue trên GitHub nếu lỗi lặp lại
- 🤝 Pair programming nếu task phức tạp

---

**🎉 Chúc các bạn làm việc nhóm thành công!**

Mọi câu hỏi, hãy comment issue hoặc liên hệ trực tiếp.

