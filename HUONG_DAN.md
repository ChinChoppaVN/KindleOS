# Hướng dẫn đẩy lên GitHub và cấu hình domain

## Bước 1: Tạo repository trên GitHub

1. Đăng nhập vào GitHub: https://github.com
2. Click nút **"+"** ở góc trên bên phải → chọn **"New repository"**
3. Điền thông tin:
   - **Repository name**: `KindleOS` (hoặc tên bạn muốn)
   - **Description**: "Web games cho Kindle Paperwhite 3"
   - Chọn **Public** (để dùng GitHub Pages miễn phí)
   - **KHÔNG** tích "Add a README file" (vì đã có sẵn)
4. Click **"Create repository"**

## Bước 2: Đẩy code lên GitHub

Sau khi tạo repository, GitHub sẽ hiển thị hướng dẫn. Chạy các lệnh sau trong terminal:

```bash
# Thêm remote repository (thay YOUR_USERNAME bằng tên GitHub của bạn)
git remote add origin https://github.com/YOUR_USERNAME/KindleOS.git

# Đổi tên branch chính thành main (nếu cần)
git branch -M main

# Đẩy code lên GitHub
git push -u origin main
```

**Lưu ý**: Nếu lần đầu push, GitHub có thể yêu cầu đăng nhập. Bạn có thể:
- Dùng Personal Access Token thay vì password
- Hoặc cấu hình SSH key

## Bước 3: Bật GitHub Pages

1. Vào repository trên GitHub
2. Click tab **"Settings"** (ở menu trên)
3. Scroll xuống phần **"Pages"** (bên trái)
4. Trong **"Source"**, chọn **"Deploy from a branch"**
5. Chọn branch **"main"** và folder **"/ (root)"**
6. Click **"Save"**
7. GitHub sẽ cung cấp URL: `https://YOUR_USERNAME.github.io/KindleOS`

## Bước 4: Cấu hình domain tùy chỉnh (kindle.ThangMedia.xyz)

### 4.1. Tạo file CNAME

Tạo file `CNAME` trong thư mục gốc với nội dung:

```
kindle.ThangMedia.xyz
```

### 4.2. Cấu hình DNS

Vào nhà cung cấp domain (nơi bạn mua ThangMedia.xyz) và thêm record DNS:

**Loại**: `CNAME`  
**Tên**: `kindle`  
**Giá trị**: `YOUR_USERNAME.github.io`  
**TTL**: `3600` (hoặc mặc định)

**HOẶC** nếu không hỗ trợ CNAME cho subdomain, dùng A record:

**Loại**: `A`  
**Tên**: `kindle`  
**Giá trị**: 
- `185.199.108.153`
- `185.199.109.153`
- `185.199.110.153`
- `185.199.111.153`

(Thêm 4 A records với 4 IP trên)

### 4.3. Commit và push file CNAME

```bash
git add CNAME
git commit -m "Add custom domain"
git push
```

### 4.4. Cập nhật cấu hình trên GitHub

1. Vào **Settings** → **Pages**
2. Trong phần **"Custom domain"**, nhập: `kindle.ThangMedia.xyz`
3. Tích **"Enforce HTTPS"** (sau khi DNS đã propagate)
4. Click **"Save"**

## Bước 5: Chờ DNS propagate

- DNS thường mất **5-30 phút** để cập nhật
- Có thể kiểm tra bằng: https://dnschecker.org
- Sau khi DNS đã propagate, website sẽ hoạt động tại: `https://kindle.ThangMedia.xyz`

## Lưu ý quan trọng

1. **HTTPS**: GitHub Pages tự động cung cấp SSL certificate miễn phí
2. **Cập nhật code**: Mỗi lần sửa code, chạy:
   ```bash
   git add .
   git commit -m "Mô tả thay đổi"
   git push
   ```
3. **Thời gian deploy**: GitHub Pages thường deploy trong 1-2 phút sau khi push

## Kiểm tra

Sau khi hoàn tất, truy cập:
- GitHub Pages URL: `https://YOUR_USERNAME.github.io/KindleOS`
- Custom domain: `https://kindle.ThangMedia.xyz`

Cả hai URL sẽ trỏ đến cùng một website!

