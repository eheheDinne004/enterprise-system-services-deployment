# CHƯƠNG III: KHẢO SÁT HỆ THỐNG MẠNG THỰC TẾ

## 3.1. Giới thiệu về doanh nghiệp
- **Quy mô:** Doanh nghiệp nhỏ gồm 10 nhân sự.
- **Cơ cấu tổ chức:**
  - 01 Giám đốc
  - 02 Nhân viên HR
  - 01 Nhân viên IT / Quản trị mạng
  - 04 Nhân viên Kinh doanh
  - 02 Nhân viên Kế toán

## 3.2. Tổng quan hệ thống mạng
### 3.2.1. Sơ đồ thiết kế logic
*(Thêm hình ảnh sơ đồ mạng tại đây bằng cách tải ảnh lên GitHub và chèn liên kết)*
`![Sơ đồ logic](./images/so-do-logic.png)`

### 3.2.2. Số lượng thiết bị sử dụng thực tế
- Server (Windows Server 2019/2022)
- Router / Switch Layer 3
- PC Client / Laptop phòng ban

### 3.2.3. Phân hoạch địa chỉ IP & VLAN các phòng ban
| Phòng ban | Số lượng máy | Subnet / VLAN | Dải IP cấp phát | Gateway |
| :--- | :---: | :---: | :--- | :--- |
| **Ban Giám đốc** | 1 | VLAN 10 | `192.168.10.0/24` | `192.168.10.1` |
| **Phòng HR** | 2 | VLAN 20 | `192.168.20.0/24` | `192.168.20.1` |
| **Phòng IT** | 1 | VLAN 30 | `192.168.30.0/24` | `192.168.30.1` |
| **Phòng Kinh doanh** | 4 | VLAN 40 | `192.168.40.0/24` | `192.168.40.1` |
| **Phòng Kế toán** | 2 | VLAN 50 | `192.168.50.0/24` | `192.168.50.1` |

---

# CHƯƠNG IV: TRIỂN KHAI GIẢI PHÁP DEMO

## 4.1. Thiết lập Domain và Domain Controller (AD DS)
- Khởi tạo Domain Name System nội bộ (`companyabc.com`).
- Elevate Windows Server lên Domain Controller.

## 4.2. Triển khai DNS Server nội bộ
- Cấu hình Forward Lookup Zone & Reverse Lookup Zone.
- Cấu hình các bản ghi A, CNAME, MX cho Web Server và Mail Server.

## 4.3. Tạo OU, Users và Groups
- Phân cấp Organizational Units (OU) theo sơ đồ phòng ban.
- Tạo người dùng đại diện và phân quyền theo Security Groups.

## 4.4. Triển khai Group Policy Objects (GPO)
- Chính sách độ phức tạp mật khẩu & thời hạn đổi mật khẩu.
- Cấu hình khóa màn hình tự động, chặn USB, ẩn Control Panel.

## 4.5. Triển khai DHCP Server (đa phòng ban)
- Cấu hình các Scope tương ứng cho từng VLAN phòng ban.
- Thiết lập DHCP Relay Agent trên Router.

## 4.6. Cấu hình VLAN & Inter-VLAN Routing
- Cấu hình Trunking/Access trên Switch.
- Cấu hình Sub-interfaces (Router-on-a-stick) cho phép định tuyến giữa các VLAN.

## 4.7. Triển khai Web Server (IIS)
- Triển khai 2 Web sites:
  1. Website tổng công ty.
  2. Website nội bộ Phòng Kinh doanh.

## 4.8. Triển khai Mail Server (MDaemon)
- Cấu hình Mail Server phục vụ gửi/nhận email nội bộ theo tên miền domain.

## 4.9. Cấu hình Firewall / ACL bảo mật hệ thống
- Thiết lập luật lọc lưu lượng giữa các phòng ban (ví dụ: Chặn VLAN Kinh doanh truy cập trực tiếp VLAN Kế toán).

## 4.10. Triển khai Backup & Failover
- Lập lịch sao lưu dữ liệu hệ thống (System State, Active Directory DB) sử dụng Windows Server Backup.
