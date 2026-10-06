# Bài 2: Cấu hình phân quyền Nhóm và sudoers bằng visudo

## Tạo Group và User

```bash
sudo groupadd devops-admin
sudo adduser deployer
sudo usermod -aG devops-admin deployer
```

Kiểm tra:

```bash
groups deployer
```

## Cấu hình sudoers

```bash
sudo visudo
```

Thêm vào cuối file:

```text
%devops-admin ALL=(ALL) NOPASSWD: /usr/bin/systemctl start *, /usr/bin/systemctl stop *, /usr/bin/systemctl restart *, /usr/bin/systemctl status *
```

## Kiểm tra bằng user deployer

```bash
su - deployer
sudo -l
sudo systemctl restart cron
sudo systemctl status cron
```

## Kết quả mong đợi

- `deployer` thuộc nhóm `devops-admin`.
- `sudo -l` hiển thị quyền chạy `systemctl start/stop/restart/status` với `NOPASSWD`.
- `sudo systemctl restart cron` chạy thành công mà không yêu cầu mật khẩu sudo.

## Minh chứng

Chèn ảnh kết quả:

```bash
sudo -l
sudo systemctl restart cron
sudo systemctl status cron
```
