# 🚀 SETUP HƯỚNG DẪN - GITHUB WORKFLOW CHO TEAM

> **Đây là hướng dẫn chi tiết cho những ai muốn fork và tham gia phát triển dự án này.**

---

## 📌 GHI CHÚNG TỚI

| Loại | Nội Dung |
|------|----------|
| **Repo Gốc** | https://github.com/hieu97499/parkingsystem_v3 |
| **Owner** | @hieu97499 |
| **Branch Chính** | `main` (production), `dev` (development) |
| **Branch Tính Năng** | `payment`, `iot-bridge`, `admin-web` |

---

## 🎯 SETUP WORKFLOW (5 BƯỚC)

### Bước 1️⃣: Fork Repo Gốc

1. Truy cập: https://github.com/hieu97499/parkingsystem_v3
2. Nhấn nút **"Fork"** (góc trên phải)
3. GitHub tạo bản sao tại: `https://github.com/YOUR_USERNAME/parkingsystem_v3`

---

### Bước 2️⃣: Clone Fork Về Máy Tính

```bash
# Bạn sẽ có URL fork như sau:
# https://github.com/YOUR_USERNAME/parkingsystem_v3

git clone https://github.com/YOUR_USERNAME/parkingsystem_v3.git C:\DoAn
cd C:\DoAn
```

---

### Bước 3️⃣: Thêm Remote "Upstream"

Điều này rất quan trọng để đồng bộ code từ repo gốc:

```bash
# Thêm remote upstream trỏ về repo gốc
git remote add upstream https://github.com/hieu97499/parkingsystem_v3.git

# Kiểm tra (phải thấy 2 remote: origin và upstream)
git remote -v

# Output mong muốn:
# origin      https://github.com/YOUR_USERNAME/parkingsystem_v3.git (fetch)
# origin      https://github.com/YOUR_USERNAME/parkingsystem_v3.git (push)
# upstream    https://github.com/hieu97499/parkingsystem_v3.git (fetch)
# upstream    https://github.com/hieu97499/parkingsystem_v3.git (push)
```

---

### Bước 4️⃣: Chọn Branch Phù Hợp

```bash
# Cập nhật tất cả branches từ upstream
git fetch upstream

# Lựa chọn branch theo phân công:
git checkout dev            # (Nếu code tổng thể)
git checkout payment        # (Thanh toán)
git checkout iot-bridge     # (Hardware & Bridge)
git checkout admin-web      # (Giao diện Admin)

# Merge với upstream để cập nhật mới nhất
git merge upstream/dev      # (Thay dev bằng branch bạn chọn)
```

---

### Bước 5️⃣: Code & Tạo Pull Request

```bash
# 1. Code thay đổi
# ... Edit files ...

# 2. Commit
git add .
git commit -m "feat: tính năng mới"

# 3. Push lên FORK của bạn
git push origin dev          # (Thay "dev" bằng branch bạn chọn)

# 4. Tạo Pull Request trên GitHub
# → Vào: https://github.com/YOUR_USERNAME/parkingsystem_v3
# → Nhấn: "Compare & pull request"
# → base: hieu97499/parkingsystem_v3 → dev
# → compare: YOUR_USERNAME/parkingsystem_v3 → dev
# → Create Pull Request
```

---

## 📋 BRANCH STRATEGIES

### Branch `main`
- ❌ **KHÔNG** commit trực tiếp vào đây
- ✅ Production-ready code
- ✅ Chỉ merge từ `dev` khi ready release
- 🏷️ Có tag version (v1.0.0, v1.1.0, ...)

### Branch `dev`
- ✅ Nơi tất cả features merge vào
- ✅ Testing trước khi release
- ✅ Có thể có code chưa stable
- ✅ **ĐÂY LÀ TỶ LỆ MERGE CHÍNH**

### Branch Feature (`payment`, `iot-bridge`, `admin-web`)
- ✅ Mỗi feature/task có 1 branch
- ✅ Merge vào `dev` thông qua PR
- ✅ Merge được xong → có thể xóa

---

## 💻 HƯỚNG DẪN HÀNG NGÀY

### Morning: Cập Nhật Code Mới

```bash
# 1. Fetch mới nhất từ upstream
git fetch upstream

# 2. Merge dev mới vào branch của bạn
git checkout payment          # (Thay payment bằng branch của bạn)
git merge upstream/dev        # Cập nhật từ repo gốc

# 3. Nếu có conflict → resolve conflict
# (Edit file → chọn phần code đúng)
git add .
git commit -m "fix: resolve merge conflicts"
```

### Afternoon: Code & Commit

```bash
# 1. Edit files
nano src/payment/service.js

# 2. Xem thay đổi
git status
git diff

# 3. Stage & Commit
git add .
git commit -m "feat: thêm integration Stripe"

# 4. Push lên fork của bạn
git push origin payment
```

### Evening: Tạo Pull Request

```bash
# 1. Trên GitHub, vào repo fork của bạn
https://github.com/YOUR_USERNAME/parkingsystem_v3

# 2. GitHub sẽ hiện notification "Compare & pull request"
# → Nhấn nút đó

# 3. Điền thông tin:
# - Title: feat: integrate Stripe payment
# - Description: 
#   - Thêm Stripe API integration
#   - Test trên staging ✅
#   - Ready for review
# - base: dev (LUÔN CHỌN DEV!)
# - compare: payment

# 4. Nhấn "Create Pull Request"
# → Chờ Owner review & merge
```

---

## 🔄 KHI CÓ CONFLICT

```bash
# 1. Update từ upstream
git fetch upstream
git merge upstream/dev

# 2. Git báo conflict → xem chi tiết
git status    # Xem file nào bị conflict

# 3. Edit file conflict
# File sẽ có dạng:
# <<<<<<< HEAD
# // Código của bạn
# =======
# // Code từ upstream
# >>>>>>> upstream/dev

# Bạn chọn phần nào, xóa marker, lưu file

# 4. Resolve & Push
git add .
git commit -m "fix: resolve merge conflicts with upstream/dev"
git push origin payment
```

---

## ✅ CHECKLIST TRƯỚC KHI PUSH

- [ ] Đã `git fetch upstream && git merge upstream/dev`?
- [ ] Code chạy mà không lỗi?
- [ ] KHÔNG có `console.log()` debug?
- [ ] KHÔNG commit `.env` hay `node_modules`?
- [ ] Commit message rõ ràng & theo format?
- [ ] Tests xanh (nếu có)?
- [ ] Đã xem diff trước push? (`git diff`)
- [ ] README/docs updated (nếu cần)?

---

## 📚 FILE QUAN TRỌNG

Sau khi clone, hãy đọc:

1. **README.md** – Tổng quan dự án
2. **TEAM_COLLABORATION_GUIDE.md** – Chi tiết workflow
3. **QUICK_START_TEAM.md** – Quick start cho từng role
4. **BuildWeb/backend/.env.example** – Cấu hình mẫu
5. **hardware/ai_service/.env.example** – Cấu hình AI

---

## 🛠️ CÔNG CỤ RECOMMENDED

| Công Cụ | Mục Đích |
|---------|----------|
| **VS Code** | Code editor |
| **Git** | Version control |
| **GitHub Desktop** | GUI cho Git (optional) |
| **Node.js** | Backend + Bridge |
| **Python 3.8+** | AI Service |
| **PostgreSQL** | Database |

---

## 🚨 LỖI THƯỜNG GẶP

### ❌ "Permission denied (publickey)"
**Giải pháp:** Setup SSH key cho GitHub
```bash
# https://docs.github.com/en/authentication/connecting-to-github-with-ssh
# Hoặc dùng HTTPS + PAT (Personal Access Token)
```

### ❌ "failed to push some refs"
**Giải pháp:** Update trước khi push
```bash
git fetch upstream
git merge upstream/dev
git push origin payment
```

### ❌ "Merge conflict"
**Giải pháp:** Resolve conflicts (xem phần trên)

### ❌ "Your branch is ahead of 'origin/payment' by 3 commits"
**Giải pháp:** Push commits
```bash
git push origin payment
```

---

## 📞 CẦN GIÚP ĐỠ?

- 📝 **Issues:** https://github.com/hieu97499/parkingsystem_v3/issues
- 💬 **Discussions:** https://github.com/hieu97499/parkingsystem_v3/discussions
- 📧 **Email:** hieu97499@gmail.com
- 💬 **Zalo/Telegram:** (liên hệ trực tiếp)

---

## 🎓 THAM KHẢO THÊM

- Git Official Book: https://git-scm.com/book
- GitHub Guides: https://guides.github.com
- Atlassian Git Tutorials: https://www.atlassian.com/git

---

**Happy Coding! 🚀**

Nếu có vấn đề gì, hãy tạo issue hoặc liên hệ trực tiếp.

