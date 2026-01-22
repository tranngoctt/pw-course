# Vòng đời luyện Git mỗi ngày (15–20 phút)

Mục tiêu: luyện **Working → Staging → Commit → Undo → Branch → Remote** để nhớ logic và hiểu bản chất.

> **Quy ước terminal:** Git Bash (MINGW64)  
> **Checkpoint bắt buộc:** sau mỗi bước lớn luôn chạy `git status` và/hoặc `git log`.

---

## 0) Chuẩn bị (chỉ làm 1 lần)
Trong repo luyện tập (vd: `git-ontap-undo/lesson03`):

```bash
mkdir -p daily
cd daily
```

---

## 1) Warm-up: Nhìn trạng thái (1 phút)

```bash
git status
git log --oneline --decorate -5
```

---

## 2) Vòng chính: Working → Staging → Commit (5 phút)

Tạo 1 file “hôm nay” và thêm 1 dòng:

```bash
touch day-$(date +%Y-%m-%d).txt
echo "note $(date)" >> day-$(date +%Y-%m-%d).txt
```

Đưa vào staging và commit:

```bash
git add .
git status
git commit -m "daily note"
git log --oneline --decorate -5
```

---

## 3) Bài 1: Sửa commit message (amend) (2 phút)

```bash
git commit --amend -m "daily note (fix msg)"
git log --oneline --decorate -5
```

---

## 4) Bài 2: Unstage 1 file (Staging → Working) (3 phút)

Tạo 3 file, add hết, rồi unstage 1 file:

```bash
touch f2.txt f3.txt f4.txt
git add .
git status
git restore --staged f3.txt
git status
```

Commit phần còn staged (để thấy “chọn lọc”):

```bash
git commit -m "add f2 f4 (f3 kept in working)"
git status
```

> `f3.txt` vẫn nằm ở Working. Hôm sau em có thể `git add f3.txt` rồi commit nốt.

---

## 5) Bài 3: Uncommit (Repository → Working) (5 phút)

Giả lập “lỡ commit nhầm” → bỏ commit gần nhất:

```bash
git log --oneline --decorate -5
git reset HEAD~1
git log --oneline --decorate -5
git status
```

Commit lại cho đúng (khép vòng đời):

```bash
git add .
git commit -m "re-commit after reset"
```

---

## 6) Branch mini (3 phút)

Tạo nhánh, commit 1 thứ nhỏ, rồi quay về main:

```bash
git switch -c practice/branch
touch branch.txt
git add branch.txt
git commit -m "branch commit"

git switch main
git log --oneline --decorate -5
```

> Nếu muốn luyện gộp nhánh vào main:

```bash
git merge practice/branch
```

---

## 7) Remote (chỉ khi đã gắn GitHub) (1 phút)

Đẩy lên GitHub theo tracking:

```bash
git push
```

Nếu gặp lỗi “remote có trước”:

```bash
git pull origin main --rebase
git push
```

---

# Quy tắc vàng để “ngấm sâu”
1) Sau mỗi thao tác lớn (add/commit/reset/restore/branch) → chạy **`git status`**.  
2) Sau mỗi thay đổi lịch sử (commit/amend/reset/merge) → chạy **`git log --oneline --decorate -5`**.  
3) Luôn tự nói 1 câu: **“Mình đang ở vùng nào? Working/Staging/Repo/Remote?”**
