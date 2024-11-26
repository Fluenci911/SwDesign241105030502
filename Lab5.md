# Thiết Kế Các Hệ Thống Con Trong Payroll System

## 1. Giới Thiệu

Hệ thống **Payroll System** được chia thành các hệ thống con nhằm quản lý các chức năng cụ thể và đảm bảo tính module hóa, dễ mở rộng và bảo trì. Tài liệu này mô tả chi tiết các hệ thống con bao gồm: **Report Subsystem**, **Employee Management Subsystem**, **Payroll Processing Subsystem**, **Authentication Subsystem**, **Payment Subsystem**, **Timecard Subsystem**, và **Purchase Order Subsystem**.

---

## 2. Các Hệ Thống Con

### 2.1. Report Subsystem

Hệ thống con này chịu trách nhiệm tạo, lưu trữ và quản lý các báo cáo.

- **Thành phần:**
  - `PayrollAdministratorUI`: Giao diện người dùng cho quản trị viên bảng lương.
  - `ReportController`: Điều phối việc tạo và lưu báo cáo.
  - `ReportGenerator`: Xử lý việc tạo báo cáo.
  - `ReportStorage`: Lưu trữ dữ liệu báo cáo.
  - `MySQL`: Cơ sở dữ liệu lưu trữ báo cáo.

- **Mô hình:**


![Diagram](https://www.planttext.com/api/plantuml/png/X95H2e9048RVFSNWKpruXJ0A8YYef0ECEeMag-oCWOGdww4ZTONSLSimQ5uMVhx_t_rdd_U7pu9QoYnr2emkU2Pm3rJaMY0eGwvOA7FXva0pYHBI9um8TbZfF4tdSPQeX4MZvFgujb2K8ZEq4OjSYU58Tmbs8aqer1AJwKTdl7whzIXmHOhiPSEySol-ymQDpTGREBcHVjb8II8LkDigs6zSG8Ob2eR8NsuJI5quTsvx_DuEUDvij1VBZvRr8T-5_u5Tkm7MzpLC_todTdnIiVdj5m000F__0m00)


---

### 2.2. Employee Management Subsystem

Hệ thống này quản lý thông tin nhân viên, bao gồm thêm mới, cập nhật và xóa nhân viên.

- **Thành phần:**
  - `EmployeeUI`: Giao diện người dùng.
  - `EmployeeController`: Điều phối các thao tác trên nhân viên.
  - `MySQL`: Cơ sở dữ liệu lưu thông tin nhân viên.

- **Mô hình:**


![Diagram](https://www.planttext.com/api/plantuml/png/R51B3e903DtFAHfMkk0AXaHTaCX22GSeJ3N4-P2PiY26axdmI5v1880OwQABzrxxNlj-lYBFwBZMIbHOtF5641nrfMn310cQ3j1a6D8wzurdqW4y17HL6YPtnO9WacVnG1GAlP_1lJNih5BanhcXKCf9iDb-uRgIoBJ6I5BqnxH3xzALt42GDEdv501wE21ZZfwMZlDD5ogiatvS89PS5aCOxbQY_wWM5_NgoKoq8Y8Z-qT-0000__y30000)

---

### 2.3. Payroll Processing Subsystem

Hệ thống xử lý lương đảm nhận tính toán và xử lý thanh toán cho nhân viên.

- **Thành phần:**
  - `PayrollInterface`: Giao diện xử lý lương.
  - `RunPayrollController`: Xử lý việc tính lương và thanh toán.
  - `BankSystemInterface`: Liên kết với hệ thống ngân hàng.
  - `MySQL`: Cơ sở dữ liệu lưu thông tin thanh toán.

- **Mô hình:**


![Diagram](https://www.planttext.com/api/plantuml/png/V54x3i8m3Drx2giJ35m1eSB2188JcDIKYZH5jZDKY9CnS2IkG5fIVghm4Zs_z_JybFlrDXD5Lb_Pv8JcY0L1kiQ6QsjXpRKXaT8LiFKxQKIfIk6SG9ZIAV4U3K5KB_j5HnkB8h3nBhBpscdx4aT_DmQjyHQLeceqVdEdPtXWAd8QcSjFTeRkkEtk-euFZbARqCIpEQ3GYdFY1Ifc0QI00YtO1V1vJjzxGwRcN69Yya6zKc0ocGxMwzI3lLj7d_fVDTJgaip8vUqtFG000F__0m00)

---

### 2.4. Authentication Subsystem

Hệ thống xác thực chịu trách nhiệm quản lý việc đăng nhập và kiểm tra thông tin người dùng.

- **Thành phần:**
  - `LoginPage`: Giao diện đăng nhập.
  - `AuthService`: Xử lý xác thực người dùng.
  - `MySQL`: Cơ sở dữ liệu lưu trữ thông tin người dùng.

- **Mô hình:**


![Diagram](https://www.planttext.com/api/plantuml/png/L8zD2i9038NtSuemArru1Md1PGMbU81qZ7MmdSea8nJfoLnu9AzWP_ohMIIGB-_nyhZTCnRq4jf6dT6Si2RGUP0ZER46nNOEob1npqAjXgk2iQmJyWSq14LNMxSPHMbl6cI6g2x9N-p8N_Ufy6TAEoO_coSsf1w1zA3NVRajD2332WKhv3-BA8FSc2uuuRSwZMyCM2oMqm29JWD5_h5MWyh8xUFhJm000F__0m00)

---

### 2.5. Payment Subsystem

Hệ thống thanh toán xử lý việc lựa chọn phương thức thanh toán và giao dịch liên quan.

- **Thành phần:**
  - `PaymentInterface`: Giao diện thanh toán.
  - `PaymentController`: Điều phối việc lựa chọn phương thức thanh toán.
  - `BankSystem`, `PickUpSystem`, `MailSystem`: Các hệ thống liên quan đến thanh toán.
  - `MySQL`: Cơ sở dữ liệu lưu trữ phương thức thanh toán.

- **Mô hình:**


![Diagram](https://www.planttext.com/api/plantuml/png/V991ReCm44NtFiM8LRl85IhKigbKf4Ge1vYOIM9X3F8C2nJbP5tqIBr2WPZ4LH2pi_z_Cvul_tx_f2pefQkjQb5NU298jjZNv0IAxi0z2zK9N1GCPPoGFw8c29RF-MAIjKNcMVfedFZ6Ml81deh9afPWoKdEJVdoEidNgCKxkggO9iTiPlp0PjGsR6I1sXfTxTjdhj1dAZjBezwr2s2EnYvWvCfH2O_znmrd8pqaUL_ilX90XWm53yWKTvXplEt9WLUHTCyFDfktv-HYQvJdw7r4j6AA4rcnFVPVCSqBggjAXsJ63_C7003__mC0)

---

### 2.6. Timecard Subsystem

Hệ thống quản lý thông tin bảng chấm công.

- **Thành phần:**
  - `TimecardInterface`: Giao diện bảng chấm công.
  - `TimecardController`: Quản lý thêm, cập nhật và xóa bảng chấm công.
  - `MySQL`: Cơ sở dữ liệu lưu trữ thông tin chấm công.

- **Mô hình:**


![Diagram](https://www.planttext.com/api/plantuml/png/R90n3i8m34NtdCBA14ElW2h1WWG3b0kuYK4LQLh5xb2Xdeo18t45QDMK8l3WmU_RNz_F-oDbmI1DwLIDveeN0dqgIZ8OB6HDpYqBbHfk2jvLUA5mHaCGDTiu6RXno3onTUKbLCvH6DU7GckZOB7yZ9lQej0_OidH3-c6JbuAQK7ls-omqu0C6nJCaMdkEEKvagc2vV60chCf1oJ9wa-2B_4iMA-EdgfJANdR__85003__mC0)

---

### 2.7. Purchase Order Subsystem

Hệ thống này quản lý các đơn đặt hàng.

- **Thành phần:**
  - `CommissionedEmployeeInterface`: Giao diện nhân viên hoa hồng.
  - `MaintainPurchaseOrderController`: Điều phối việc thêm, cập nhật và xóa đơn hàng.
  - `PurchaseOrderDatabase`: Cơ sở dữ liệu lưu trữ đơn hàng.

- **Mô hình:**


![Diagram](https://www.planttext.com/api/plantuml/png/X95B2i8m48RtFSNGbIwyWeZLXGjHz0JJPDHY7YKpNHJnP2uyabSmZHOLGGUICAzlyYUtotN2Wa4QQx8QrH7t1Fcw2Ug0JB0AcW9icv9R5h8vd3A8LZcXi4D5K7XhA-RAEz9pMnlV4YtwRAfL1fbXYR4dhfwSm8Lt4hmnSSI3cmorJjd1y1LhQer2Ns5DXZx3vxIJaqhQbuvKCKF1QNHoG8REAJk5RuCVOZUaVD3yfANZfqWOZSR_v2NAloVeEFsridCs8QUxJxa3003__mC0)

---

## 3. Kết Luận

Tài liệu trên đã mô tả chi tiết thiết kế từng hệ thống con trong **Payroll System**. Với cách phân chia này, hệ thống trở nên dễ quản lý, mở rộng và bảo trì hơn trong quá trình phát triển.  