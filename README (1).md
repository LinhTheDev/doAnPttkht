# DA-PTTKHT — Hướng dẫn cộng tác chỉnh sửa file Word bằng Git/GitHub

> **Dành cho thành viên thứ hai (và các thành viên khác) của dự án.** Đọc phần **Quy tắc quan trọng** trước khi sửa tài liệu.

## 1. Thông tin dự án

| Mục | Thông tin |
|---|---|
| Repository | <https://github.com/LinhTheDev/doAnPttkht> |
| Chủ sở hữu | `LinhTheDev` |
| Nhánh làm việc chính | `main` (sau khi chủ repo đã tạo và push nhánh này) |
| File Word chung | `DA_PTTKHT.docx` (**dấu gạch dưới `_`**) |
| Công cụ | Git for Windows, Microsoft Word, PowerShell hoặc Terminal của VS Code |

Mục đích: hai người đóng góp nội dung vào cùng một tài liệu Word, đồng thời dùng Git để lưu lịch sử phiên bản và đồng bộ lên GitHub.

> **Lưu ý:** `.docx` là file nhị phân. Git biết file đã thay đổi, nhưng không tự động so sánh/gộp từng đoạn văn giống file mã nguồn. **Không được để hai người cùng sửa hai bản sao của file này mà chưa phối hợp.**

## 2. Quy tắc quan trọng — cần tuân thủ

1. **Hỏi nhóm trước khi chỉnh sửa** `DA_PTTKHT.docx`. Chỉ **một người sửa file tại một thời điểm** nếu dùng Git trực tiếp.
2. **Trước khi mở Word:** đảm bảo không có thay đổi chưa lưu, sau đó chạy `git pull --ff-only origin main` để lấy bản mới nhất.
3. **Trong khi sửa:** chỉ sửa phần được phân công; không đổi tên hoặc di chuyển file Word khi chưa thống nhất.
4. **Sau khi sửa:** nhấn **Ctrl + S**, **đóng Microsoft Word**, kiểm tra file rồi mới `git add` → `git commit` → `git push`.
5. **Sau khi push thành công:** báo cho người còn lại biết để họ `pull` trước khi bắt đầu lượt chỉnh sửa tiếp theo.
6. **Không dùng** `git push --force`, `git reset --hard`, `git clean -fd` hoặc giải quyết xung đột bằng cách tùy tiện ghi đè file Word.
7. **Không dùng `git add .` một cách máy móc:** chỉ thêm file cần commit, tránh file tạm của Word và các tài liệu riêng.
8. Nếu thấy xung đột, lỗi hoặc có thay đổi của cả hai người: **dừng lại và hỏi người quản lý repo**, không thử lệnh xóa/reset khi chưa sao lưu.

## 3. Lần đầu tham gia (thành viên thứ hai)

### Bước 1 — Nhận lời mời vào Repository

Chủ repo vào **Settings → Collaborators → Add people**, nhập tài khoản GitHub của bạn. Bạn cần **chấp nhận lời mời** trong GitHub/email. Nếu repo là private, bạn sẽ không clone được khi chưa có quyền.

### Bước 2 — Cài đặt công cụ

- Cài **Git for Windows**: <https://git-scm.com/downloads/win>.
- Cài **Microsoft Word** để mở và sửa `.docx`.
- Có thể dùng **VS Code → Terminal → New Terminal** (PowerShell) để chạy Git.

Kiểm tra Git:

```powershell
git --version
```

Cấu hình tên và email cho commit (chỉ cần làm một lần trên máy; thay bằng thông tin của bạn):

```powershell
git config --global user.name "Ho Ten Cua Ban"
git config --global user.email "email-cua-ban@example.com"
```

### Bước 3 — Clone Repository về máy

**Chỉ clone sau khi chủ repo đã push commit đầu tiên lên GitHub.** Chọn vị trí chưa có thư mục `DA-PTTKHT`:

```powershell
cd D:\
git clone https://github.com/LinhTheDev/doAnPttkht.git DA-PTTKHT
cd .\DA-PTTKHT
```

Nếu máy bạn đã có thư mục `D:\DA-PTTKHT` chứa dữ liệu, **không clone đè lên thư mục đó**: chọn thư mục trống khác, chẳng hạn `D:\DA-PTTKHT-Nguoi2`.

**Sau khi clone, không cần chạy `git init` và không cần `git remote add origin`.** Clone đã thực hiện các bước đó.

Xác minh:

```powershell
git status
git remote -v
git branch --show-current
Get-ChildItem
```

Kỳ vọng: remote trỏ về `LinhTheDev/doAnPttkht`, nhánh là `main`, có file `DA_PTTKHT.docx` và không có thay đổi cục bộ (`working tree clean`). Nếu chưa có file, nhắn cho chủ repo kiểm tra commit/push đầu tiên.

## 4. Quy trình chuẩn mỗi lần chỉnh sửa Word

### A. Trước khi sửa

1. Nhắn trong nhóm: **"Mình bắt đầu sửa [Chương/Mục ...]. Mọi người tạm không chỉnh `DA_PTTKHT.docx` đến khi mình báo đã push xong."**
2. Đảm bảo Word đã đóng và đang đứng trong thư mục clone.
3. Kiểm tra tình trạng và cập nhật từ GitHub:

```powershell
cd D:\DA-PTTKHT
git status
git switch main
git pull --ff-only origin main
git log -3 --oneline
```

> Đường dẫn `D:\DA-PTTKHT` là **ví dụ**. Đổi thành thư mục clone thật của bạn. Chỉ chạy `pull` khi không có thay đổi cục bộ cần giữ. Nếu `git status` báo modified/untracked không rõ nguyên nhân, hãy kiểm tra trước khi tiếp tục.

### B. Trong khi sửa

1. Mở `DA_PTTKHT.docx` bằng Microsoft Word.
2. Chỉnh nội dung phần được giao; giữ nguyên bố cục, heading, mục lục và định dạng chung nếu không được yêu cầu đổi.
3. Lưu với **Ctrl + S**. Kiểm tra file mở lại được, hình ảnh/bảng không bị lỗi.
4. **Đóng Word hoàn toàn** trước khi commit (tránh file khóa tạm và dữ liệu chưa ghi hết).

### C. Sau khi sửa — commit và push

Trong PowerShell tại thư mục clone:

```powershell
git status
git add -- "DA_PTTKHT.docx"
git diff --cached --stat
git commit -m "Cap nhat chuong 2 - bo sung noi dung"
git push origin main
git status
```

- Thay nội dung thông báo commit theo phần thực tế bạn sửa.
- `git add -- "DA_PTTKHT.docx"`: chỉ đưa đúng file Word vào staging.
- `git commit`: **lưu phiên bản trên máy**; **chưa** có nghĩa là GitHub đã nhận được bản mới.
- `git push`: tải commit lên GitHub. Nếu chưa `push` thành công, người còn lại chưa thể `pull` thay đổi của bạn.
- `git status` sau cùng lý tưởng hiển thị `nothing to commit, working tree clean` (nếu không có các file khác chưa theo dõi).

**Xác nhận trên GitHub:** mở <https://github.com/LinhTheDev/doAnPttkht>, chọn nhánh `main`, kiểm tra commit mới trong lịch sử. GitHub có thể không hiển thị toàn bộ nội dung `.docx` trực tiếp; tải file về/mở Word để kiểm tra nếu cần.

**Cuối lượt:** nhắn trong nhóm: **"Mình đã sửa [mục...], commit `<mã commit>`, push thành công. Mọi người có thể pull và tiếp tục."** Xem mã commit bằng `git log -1 --oneline`.

## 5. Quy trình chuyển lượt giữa hai người (quan trọng)

Ví dụ:

1. **Người A** báo đang chỉnh Chương 1 → sửa → lưu/đóng Word → commit → push → thông báo hoàn tất.
2. **Người B** chờ A hoàn tất, chạy `git pull --ff-only origin main` **trước khi mở Word** → chỉnh Chương 2 → commit → push → thông báo hoàn tất.
3. **Người A** muốn làm tiếp phải `pull` bản mới trước, không mở bản Word cũ đã có sẵn trong máy để ghi đè.

| Thời điểm | Người A | Người B |
|---|---|---|
| Lượt 1 | Chỉnh sửa, commit, push | Chờ / làm việc khác |
| Lượt 2 | Chờ / pull bản mới sau khi B push | Pull bản A, chỉnh sửa, commit, push |
| Lượt 3 | Pull bản B rồi chỉnh sửa | Chờ / làm việc khác |

**Muốn sửa đồng thời:** hãy dùng **Word trên OneDrive/SharePoint** để đồng biên tập, rồi giao một người lưu phiên bản đã chốt về `DA_PTTKHT.docx` và commit/push lên GitHub. Hoặc tách các chương thành các file `.docx` khác nhau và thống nhất cách ghép sau. Tạo hai nhánh Git riêng **không tự giải quyết** xung đột khi cả hai sửa **cùng một `.docx`**.

## 6. Những lệnh Git cần biết

| Lệnh | Tác dụng |
|---|---|
| `git status` | Xem file nào mới, đã sửa, đã stage |
| `git pull --ff-only origin main` | Lấy bản mới nhất khi có thể cập nhật thẳng, không tạo merge commit |
| `git add -- "DA_PTTKHT.docx"` | Chọn file Word để commit |
| `git commit -m "Mo ta thay doi"` | Tạo mốc phiên bản trong máy |
| `git push origin main` | Đẩy các commit lên GitHub |
| `git log --oneline -10` | Xem 10 commit gần nhất |
| `git show --stat HEAD` | Xem danh sách file thay đổi ở commit mới nhất |
| `git diff --stat` | Kiểm tra file nào thay đổi; không hiện nội dung bên trong `.docx` |
| `git remote -v` | Kiểm tra URL GitHub đang kết nối |
| `git branch --show-current` | Xem nhánh hiện tại |

Ví dụ thông điệp commit tốt:

```text
Cap nhat chuong 1 - bo sung muc tieu de tai
Chinh sua so do va bang mo ta chuong 2
Sua loi chinh ta va dinh dang bao cao
```

Không nên đặt kiểu `update`, `fix`, `123` vì khó truy lại thay đổi sau này.

## 7. Một số lỗi thường gặp và cách xử lý an toàn

### `fatal: not a git repository`

Bạn đang mở Terminal ngoài thư mục đã clone. Dùng `cd` đến đúng thư mục rồi chạy `git status`. Không tạo thêm `.git` mới trong thư mục đang clone.

### `fatal: destination path ... already exists`

Thư mục đích clone đã tồn tại. Chọn **tên thư mục mới, trống** hoặc kiểm tra thư mục cũ trước. Không xóa dữ liệu chỉ để chạy lại lệnh.

### `nothing to commit, working tree clean`

Không có thay đổi nào để commit. Kiểm tra bạn đã **Ctrl + S**, đóng Word, và sửa đúng file trong thư mục clone chưa.

### `rejected (fetch first)` / `non-fast-forward` khi push

Có thể người khác vừa push trước bạn. **Không dùng `git push --force`.** Vì `.docx` khó merge, hãy giữ bản của bạn, sao lưu file ra **ngoài thư mục repo**, thông báo với nhóm và cùng kiểm tra các phiên bản trước khi đồng bộ.

### `fatal: Not possible to fast-forward, aborting` khi pull

Lịch sử ở máy và GitHub đã tách nhánh. **Không tự `reset --hard`, merge hoặc rebase** khi đang dùng file Word chung. Báo chủ repo và sao lưu file trước khi giải quyết.

### `Permission denied`, `Repository not found` khi clone/push

Kiểm tra bạn đã chấp nhận lời mời collaborator chưa, có đăng nhập **đúng tài khoản GitHub** không, URL remote có đúng không và Git Credential Manager có yêu cầu đăng nhập trên trình duyệt không. Không gửi mật khẩu/token cho người khác.

### `~$...docx` xuất hiện khi mở Word

Đó thường là file khóa/tạm của Microsoft Word; **không commit**. Chủ repo nên tạo `.gitignore` chứa:

```gitignore
# File khoa/tam Microsoft Office
~$*
*.tmp

# File he thong
Thumbs.db
.DS_Store
```

Nếu file tạm từng được thêm vào Git, chỉ thêm `.gitignore` là chưa đủ để ngừng theo dõi file đã track; hãy nhờ chủ repo xử lý riêng.

### Muốn bỏ chỉnh sửa chưa commit

**Cảnh báo: thao tác sau làm mất nội dung Word chưa commit.** Trước tiên sao chép bản cần giữ ra ngoài thư mục repo, đóng Word, xác nhận đúng file rồi mới cân nhắc:

```powershell
git restore -- "DA_PTTKHT.docx"
```

Nếu đã commit/push, **không dùng lệnh này để xóa lịch sử**. Trao đổi với chủ repo để tạo commit khôi phục phiên bản phù hợp.

## 8. An toàn dữ liệu và quản lý tài liệu

- Chỉ push file được phép chia sẻ; kiểm tra dữ liệu cá nhân, số điện thoại, chữ ký, thông tin nhạy cảm trong Word.
- Repository **public** có thể cho người khác tải file và cả lịch sử phiên bản; nếu là báo cáo nội bộ, cân nhắc repo **private**.
- Không sửa trực tiếp cùng một file trên hai máy mà chưa nhận lượt chỉnh sửa.
- Không xóa file mẫu (`MAU BAO CAO STYLE WORD.docx`, `Template_Do an Phan tich Thiet ke HTTT_2026.doc`) khi chưa có thống nhất. **Những file chưa được commit/push thì người clone sẽ không nhận được.**
- Git không thay thế bản sao lưu độc lập; nên lưu một bản dự phòng quan trọng ngoài thư mục repo.
- Nếu file Word lớn hoặc có nhiều hình, lịch sử Git sẽ tăng dung lượng theo các lần commit.

## 9. Checklist cho thành viên thứ hai

**Lần đầu:**

- [ ] Đã được mời và chấp nhận quyền collaborator.
- [ ] Đã cài Git và Microsoft Word.
- [ ] Đã cấu hình `user.name` và `user.email`.
- [ ] Đã clone đúng Repository và thấy `DA_PTTKHT.docx`.
- [ ] Đã kiểm tra đang ở nhánh `main`.

**Mỗi lần chỉnh sửa:**

- [ ] Đã báo người còn lại và được phân lượt chỉnh sửa.
- [ ] Đã kiểm tra `git status` và `pull` bản mới nhất **trước khi mở Word**.
- [ ] Đã sửa đúng phần được giao, lưu (`Ctrl + S`) và đóng Word.
- [ ] Đã kiểm tra `git status`, chỉ stage file cần thiết.
- [ ] Đã commit với nội dung mô tả rõ ràng.
- [ ] Đã `push` thành công lên `main`.
- [ ] Đã kiểm tra commit trên GitHub và thông báo cho nhóm.

---

### Tài liệu tham khảo chính thức

- [GitHub — Mời cộng tác viên](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository)
- [GitHub — Clone repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)
- [GitHub — Quy trình cộng tác](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project)

**Nguyên tắc nhớ nhanh: `Nhận lượt → Pull → Mở Word và sửa → Save + Đóng Word → Status → Add → Commit → Push → Báo nhóm`.**
