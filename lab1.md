# Phân tích kiến trúc hệ thống Payroll

## 1. Đề xuất kiến trúc

Hệ thống Payroll của Acme cần một kiến trúc **n-tầng (n-tier)** để phân chia các thành phần khác nhau, giúp dễ dàng quản lý, mở rộng và bảo trì. Kiến trúc này thường bao gồm các thành phần chính sau:

1. **Tầng giao diện người dùng (Presentation Layer)**: 

   - Chịu trách nhiệm xử lý tương tác với người dùng. 

   - Tầng này sẽ cung cấp giao diện Windows-based để nhân viên nhập thông tin chấm công, đơn hàng và truy xuất các báo cáo.

   - Tầng này bao gồm các forms, màn hình, bảng điều khiển và các tương tác UI/UX khác.

2. **Tầng logic nghiệp vụ (Business Logic Layer)**: 

   - Xử lý các quy tắc nghiệp vụ như tính lương, tính hoa hồng, xác thực thông tin và áp dụng chính sách overtime cho nhân viên theo giờ.

   - Quản lý quá trình thanh toán và tích hợp với hệ thống khác (như DB2).

   - Đảm bảo rằng các hành động như tính lương, ghi nhận giờ làm và đơn hàng được thực hiện đúng theo chính sách công ty.

3. **Tầng dữ liệu (Data Access Layer)**: 

   - Chịu trách nhiệm kết nối với các cơ sở dữ liệu (cả mới và cũ).

   - Hệ thống sẽ cần kết nối đến cơ sở dữ liệu Project Management (DB2) để lấy thông tin dự án mà không thay đổi dữ liệu ở đó.

   - Lưu trữ và quản lý thông tin của nhân viên như thông tin chấm công, đơn hàng, phương thức thanh toán, báo cáo.

4. **Tầng dịch vụ tích hợp (Integration Layer)**: 

   - Được sử dụng để kết nối hệ thống payroll với các hệ thống khác, cụ thể là DB2 Project Management Database.

   - Tầng này đảm bảo tính tương tác, xử lý thông tin từ các hệ thống bên ngoài mà không làm ảnh hưởng đến dữ liệu và nghiệp vụ nội bộ.

## 2. Lý do lựa chọn kiến trúc n-tầng

- **Tính bảo trì và mở rộng**: Kiến trúc n-tầng cho phép dễ dàng thay đổi hoặc thêm chức năng mà không ảnh hưởng đến các tầng khác.

- **Phân tách nhiệm vụ**: Mỗi tầng sẽ chịu trách nhiệm cho một phần công việc cụ thể (giao diện, nghiệp vụ, truy cập dữ liệu), giúp đơn giản hóa quy trình phát triển.

- **Bảo mật**: Phân tầng rõ ràng giúp dễ dàng kiểm soát truy cập và bảo mật, ví dụ như bảo mật ở tầng giao diện người dùng và tầng truy cập dữ liệu.

- **Tích hợp dễ dàng**: Dễ dàng kết nối với các hệ thống khác, chẳng hạn như hệ thống DB2 hiện tại.

## 3. Ý nghĩa từng thành phần

- **Presentation Layer**: Hiển thị giao diện cho người dùng, thu thập và hiển thị thông tin như chấm công, đơn hàng.

- **Business Logic Layer**: Thực hiện các quy tắc nghiệp vụ như tính lương, ghi nhận thông tin nhân viên, xác thực dữ liệu.

- **Data Access Layer**: Truy xuất và quản lý dữ liệu nhân viên, kết nối với hệ thống DB2 để lấy thông tin dự án.

- **Integration Layer**: Kết nối và xử lý thông tin giữa các hệ thống khác nhau mà không ảnh hưởng đến dữ liệu nội bộ.

## 4. Biểu đồ Package mô tả kiến trúc

![Diagram](https://www.planttext.com/api/plantuml/png/T991ReCm44NtdCBAFfiUe0efLHKf4gXDLr4M8pEYLh6DnYOHYdAoB7gaNg6486fWmixVNs_iPtwlFoldWNojooYgG7v3WMAH4Jeq7hooHcoXGLg8SoJQR_-ggz8sY9-Rmps8SwtCRNK90ElQAOFEYQqjb9mWCcZ8bkK7qb59x34lLclbN3jmdAT79AyqZjDth2pv8Gj79-11n59sqzcZ9t7QOtOjM0Bb_qbMa_m2XodbI5qSiZV6Oq6SbcJz56mUXelgLkCRU3n1qw52VsAvV9xR68G-s9u4zzRC4bzZ9FF5aIg-CdB7aFlZptpojCc3Jdq-TX4AvblH2ar--x__0000__y30000)

### Giải thích biểu đồ:

Presentation Layer

- EmployeeUI: Giao diện cho nhân viên để nhập thông tin chấm công và đơn đặt hàng. Nhân viên chỉ có thể truy cập và chỉnh sửa thông tin của chính mình.

- AdminUI: Giao diện cho quản trị viên để quản lý thông tin nhân viên, thêm mới, xóa nhân viên, và chạy các báo cáo quản trị.

Business Logic Layer

- PayrollService: Thành phần nghiệp vụ chính chịu trách nhiệm tính lương cho nhân viên dựa trên loại hình thanh toán (lương giờ, lương cố định, hoa hồng). Nó cũng quản lý thông tin về giờ làm, đơn hàng và các loại hình thanh toán.

- OvertimeService: Thành phần này xử lý các quy tắc về giờ làm thêm và tính toán tiền làm thêm giờ cho nhân viên khi họ làm hơn 8 giờ trong ngày.

- CommissionService: Xử lý việc tính hoa hồng dựa trên các đơn hàng mà nhân viên bán hàng đã nhập vào hệ thống. Hoa hồng có thể là 10%, 15%, 25% hoặc 35% dựa trên quy định của công ty.

- ReportService: Cung cấp các báo cáo chi tiết cho cả nhân viên và quản trị viên, bao gồm tổng số giờ làm, doanh thu từ các dự án, tổng số tiền đã nhận và thời gian nghỉ phép còn lại.

Data Access Layer

- EmployeeDAO: Truy xuất và lưu trữ dữ liệu về thông tin nhân viên như tên, địa chỉ, và loại hình thanh toán.

- TimecardDAO: Quản lý dữ liệu chấm công, bao gồm số giờ làm việc và ngày làm việc cho nhân viên.

- PurchaseOrderDAO: Xử lý thông tin đơn hàng liên quan đến các nhân viên bán hàng, lưu trữ ngày và giá trị đơn hàng.

Integration Layer

- DB2Integration: Tích hợp với cơ sở dữ liệu Project Management hiện tại (DB2) để truy vấn thông tin về các dự án và charge numbers. Lưu ý rằng hệ thống không thay đổi dữ liệu trong DB2, chỉ truy vấn dữ liệu cần thiết.

- PaymentGateway: Thành phần này xử lý việc thanh toán cho nhân viên theo các phương thức mà họ lựa chọn, bao gồm chuyển khoản ngân hàng hoặc gửi phiếu lương đến địa chỉ.


# Cơ chế phân tích

Dưới đây là các cơ chế cần giải quyết trong bài toán Payroll và lý do lựa chọn từng cơ chế.

## 1. Cơ chế bảo mật và phân quyền

### Lý do:

- **Bảo vệ thông tin nhân viên**: Do nhân viên chỉ có thể truy cập và chỉnh sửa thông tin của riêng mình (ví dụ: thông tin chấm công và đơn hàng), hệ thống cần một cơ chế bảo mật chặt chẽ để ngăn chặn người dùng không có thẩm quyền truy cập vào dữ liệu của người khác.

- **Tính bảo mật cao cho hệ thống**: Vì hệ thống xử lý thông tin tài chính nhạy cảm (lương, hoa hồng), cần đảm bảo rằng chỉ các quản trị viên mới có quyền thêm, xóa hoặc chỉnh sửa thông tin của tất cả nhân viên.

### Giải pháp đề xuất:

- **Cơ chế phân quyền (Authorization)**: Áp dụng các cấp độ quyền khác nhau cho người dùng. Chẳng hạn, nhân viên thường chỉ có quyền xem và sửa thông tin của mình, còn quản trị viên có quyền quản lý toàn bộ dữ liệu.

- **Xác thực người dùng (Authentication)**: Sử dụng cơ chế đăng nhập an toàn với tên đăng nhập và mật khẩu hoặc tích hợp với hệ thống xác thực đa yếu tố (MFA) để đảm bảo người dùng là người có quyền truy cập hợp lệ.

- **Mã hóa dữ liệu (Data Encryption)**: Mã hóa các thông tin nhạy cảm như thông tin cá nhân và tài chính để bảo vệ khi truyền tải qua mạng hoặc lưu trữ.

## 2. Cơ chế tính lương và hoa hồng

### Lý do:

- **Đảm bảo tính chính xác**: Hệ thống cần tính lương cho nhân viên dựa trên loại hình thanh toán (theo giờ, lương cố định, hoặc có hoa hồng) và tuân theo các chính sách nội bộ của công ty (ví dụ: trả lương overtime cho nhân viên theo giờ khi họ làm quá 8 giờ một ngày).

- **Tính tự động hóa**: Hệ thống phải tự động tính toán lương và phát hành phiếu lương mà không cần can thiệp thủ công.

### Giải pháp đề xuất:

- **Cơ chế tính lương theo giờ (Hourly Payment Calculation)**: Xử lý việc tính toán số giờ làm việc của nhân viên và áp dụng chính sách overtime khi số giờ làm việc vượt quá 8 giờ/ngày.

- **Cơ chế tính lương cố định (Salaried Payment Calculation)**: Xử lý việc trả lương cố định cho nhân viên hàng tháng, mặc dù vẫn ghi nhận thông tin chấm công.

- **Cơ chế tính hoa hồng (Commission Calculation)**: Xử lý việc tính toán hoa hồng cho nhân viên bán hàng dựa trên tổng giá trị đơn hàng và tỷ lệ hoa hồng được áp dụng (10%, 15%, 25%, 35%).

## 3. Cơ chế tạo báo cáo

### Lý do:

- **Yêu cầu từ phía người dùng**: Một trong những yêu cầu quan trọng của hệ thống là khả năng tạo các báo cáo về số giờ làm việc, tổng lương đã nhận, số giờ làm thêm, doanh số bán hàng, và thời gian nghỉ phép còn lại của nhân viên.

- **Hỗ trợ quản lý**: Các báo cáo giúp cả nhân viên và quản trị viên theo dõi hiệu suất làm việc và tổng quan về tài chính.

### Giải pháp đề xuất:

- **Cơ chế tạo báo cáo động (Dynamic Reporting)**: Hệ thống cần cung cấp chức năng tạo các báo cáo động, cho phép người dùng tự chọn phạm vi thời gian và các tiêu chí báo cáo.

- **Tùy chỉnh báo cáo (Customizable Reports)**: Cho phép nhân viên và quản trị viên tùy chỉnh các báo cáo để phục vụ mục đích riêng (như báo cáo lương, giờ làm thêm, hoặc doanh thu bán hàng).

- **Lưu trữ lịch sử báo cáo (Historical Data Reports)**: Lưu trữ dữ liệu lịch sử để người dùng có thể xem lại các báo cáo từ các khoảng thời gian trước đó, giúp phân tích xu hướng làm việc và doanh số.

## 4. Cơ chế tích hợp với hệ thống hiện có

### Lý do:

- **Sử dụng cơ sở dữ liệu hiện tại**: Công ty muốn tiếp tục sử dụng hệ thống Project Management Database (DB2) hiện tại, do đó cần một cơ chế tích hợp với hệ thống này mà không làm thay đổi dữ liệu của nó.

- **Bảo vệ dữ liệu quan trọng**: Việc không thay đổi dữ liệu trong hệ thống DB2 giúp đảm bảo tính toàn vẹn của dữ liệu và duy trì hệ thống cũ mà không cần thay đổi lớn.

### Giải pháp đề xuất:

- **Cơ chế truy vấn không thay đổi (Read-Only Integration)**: Thiết lập cơ chế truy vấn đọc dữ liệu từ DB2 nhưng không có quyền thay đổi dữ liệu, đảm bảo an toàn và tương thích với hệ thống hiện tại.

- **API giao tiếp (API Integration)**: Sử dụng các API để kết nối giữa hệ thống Payroll và DB2, lấy thông tin dự án và charge number để phục vụ cho tính toán lương và phân bổ giờ làm.

## 5. Cơ chế thanh toán

### Lý do:

- **Sự linh hoạt trong phương thức thanh toán**: Nhân viên có thể lựa chọn cách thức nhận lương qua chuyển khoản, phiếu lương qua bưu điện, hoặc nhận trực tiếp tại văn phòng.

- **Tính tự động hóa**: Hệ thống phải tự động hóa quá trình thanh toán, phát lương vào các ngày quy định (thứ 6 hàng tuần và ngày cuối cùng của tháng).

### Giải pháp đề xuất:

- **Cơ chế thanh toán qua ngân hàng (Direct Deposit)**: Hỗ trợ thanh toán trực tiếp qua tài khoản ngân hàng của nhân viên khi họ lựa chọn phương thức này.

- **Cơ chế tạo phiếu lương (Paycheck Generation)**: Tạo phiếu lương tự động và gửi qua email hoặc qua bưu điện theo lựa chọn của nhân viên.

- **Cơ chế phát lương tự động (Automated Payment)**: Hệ thống cần tự động chạy vào ngày thanh toán được chỉ định mà không cần can thiệp thủ công từ Payroll Administrator.

## 6. Cơ chế lưu trữ và sao lưu dữ liệu

### Lý do:

- **Đảm bảo tính toàn vẹn dữ liệu**: Hệ thống Payroll cần phải lưu trữ thông tin chính xác về giờ làm, đơn hàng, và lịch sử thanh toán của nhân viên.

- **Khôi phục khi gặp sự cố**: Cần có cơ chế sao lưu dữ liệu thường xuyên để bảo đảm có thể khôi phục hệ thống khi gặp sự cố như hỏng hóc phần cứng hoặc tấn công bảo mật.

### Giải pháp đề xuất:

- **Cơ chế sao lưu tự động (Automatic Backup)**: Tự động sao lưu dữ liệu Payroll vào các khoảng thời gian nhất định (hàng ngày, hàng tuần) để đảm bảo tính an toàn.

- **Lưu trữ dữ liệu lịch sử (Historical Data Storage)**: Lưu trữ dữ liệu về thời gian làm việc, đơn hàng và lịch sử thanh toán của nhân viên để đảm bảo có thể truy xuất dữ liệu khi cần.


# Phân tích ca sử dụng Payment

Trong phần này, em sẽ phân tích ca sử dụng (Use Case) "Payment" nhằm hiểu rõ các lớp liên quan, hành vi của hệ thống thông qua biểu đồ sequence, và xác định các nhiệm vụ, thuộc tính, cũng như mối quan hệ giữa các lớp phân tích.

## 1. Xác định các lớp phân tích cho ca sử dụng Payment

Trong hệ thống Payroll, ca sử dụng Payment chịu trách nhiệm tính toán và xử lý việc trả lương cho nhân viên. Các lớp phân tích chính cho ca sử dụng này bao gồm:

### 1.1 Lớp `Employee`

- **Nhiệm vụ**: Đại diện cho nhân viên trong hệ thống.

- **Thuộc tính**:

  - `employeeID`: Mã số nhân viên.

  - `name`: Tên nhân viên.

  - `paymentClassification`: Loại thanh toán của nhân viên (theo giờ, cố định, hoa hồng).

  - `paymentMethod`: Phương thức thanh toán mà nhân viên chọn (chuyển khoản, nhận tại văn phòng, gửi qua bưu điện).

  - `paymentSchedule`: Lịch trình trả lương (hàng tuần, cuối tháng).
  
### 1.2 Lớp `Payment`

- **Nhiệm vụ**: Chịu trách nhiệm quản lý việc trả lương, bao gồm tính toán và phát hành phiếu lương cho nhân viên.

- **Thuộc tính**:

  - `paymentID`: Mã giao dịch thanh toán.

  - `amount`: Số tiền lương được thanh toán.

  - `paymentDate`: Ngày thanh toán.

### 1.3 Lớp `Timecard`

- **Nhiệm vụ**: Quản lý thông tin chấm công của nhân viên làm việc theo giờ, dùng để tính toán lương dựa trên số giờ làm việc.

- **Thuộc tính**:

  - `timecardID`: Mã chấm công.

  - `date`: Ngày làm việc.

  - `hoursWorked`: Số giờ làm việc.

### 1.4 Lớp `Commission`

- **Nhiệm vụ**: Chịu trách nhiệm quản lý thông tin hoa hồng cho nhân viên bán hàng.

- **Thuộc tính**:

  - `commissionRate`: Tỷ lệ hoa hồng.

  - `salesAmount`: Tổng số tiền bán hàng.

### 1.5 Lớp `PaymentMethod`

- **Nhiệm vụ**: Quản lý phương thức thanh toán mà nhân viên lựa chọn (chuyển khoản ngân hàng, phiếu lương qua bưu điện, nhận trực tiếp).

- **Thuộc tính**:

  - `methodType`: Loại phương thức thanh toán.

  - `bankAccount`: Số tài khoản ngân hàng (nếu thanh toán qua chuyển khoản).

### 1.6 Lớp `PayrollAdministrator`

- **Nhiệm vụ**: Quản trị viên chịu trách nhiệm quản lý thông tin nhân viên và xử lý các yêu cầu liên quan đến tính lương, chạy hệ thống thanh toán hàng tuần hoặc hàng tháng.

- **Thuộc tính**:

  - `adminID`: Mã quản trị viên.

### 1.7 Lớp `ProjectManagement`

- **Nhiệm vụ**: Lấy thông tin về dự án và số charge number để gán giờ làm việc của nhân viên vào từng dự án, phục vụ cho việc tính toán lương và chi phí.

- **Thuộc tính**:

  - `projectID`: Mã dự án.

  - `chargeNumber`: Mã charge number.

## 2. Biểu đồ Sequence cho ca sử dụng Payment

Biểu đồ sequence dưới đây mô tả luồng hoạt động khi hệ thống xử lý thanh toán cho nhân viên theo giờ làm việc:

  ![Diagram](https://www.planttext.com/api/plantuml/png/R99DJiCm44RtFiLSe1V80XKL12oA449YFTX3Q_1FD1ulUZOM78aha1BRaKcN-V8--yqaFr_VsoJ8ahrJg2KoFE69etFNnjjWap1EeHedn6exOX2uzQEB9w8kd5gUWdJPY_MaaKqFSlmWBNiCUA1LfHop9pb6ezGb5zXSDOK1xcWHgcru2EzHjNJYgydCroUu8K7hach1XAxyvixkY7mWUCp-ZLYj8DXqjpoJP0x_IiijtGI5lO-P4xn6_YJJkPUX1jYXqzcXj3bLdNUXviNDolLjMMP7_3cqaul2vK95LnzYEEzAKqhDPql1d7-aNm000F__0m00)

### Giải thích biểu đồ Sequence:

- Payroll Administrator khởi động quy trình trả lương, yêu cầu lấy thông tin thanh toán của nhân viên.

- Employee cung cấp thông tin từ Timecard về giờ làm việc của họ.

- Timecard tương tác với ProjectManagement để lấy thông tin charge number, sau đó trả về số giờ làm việc đã ghi nhận.

- Employee chuyển tiếp thông tin giờ làm việc đến lớp Payment để tính toán số tiền lương.

- Payment yêu cầu PaymentMethod để xác định phương thức thanh toán.

- PaymentMethod trả về phương thức thanh toán đã chọn (chuyển khoản ngân hàng, nhận trực tiếp, hoặc qua bưu điện).

- Payment xử lý thanh toán và hoàn tất quy trình trả lương.

## 3. Biểu đồ lớp phân tích (Class Diagram)

![Diagram](https://www.planttext.com/api/plantuml/png/T5BBRiCW4Bpp5SZ7IewQQqwfcXvwI5GfaN9UmzQcuM5XE5XHlwo7Vb9_eS76AQJn2StkC3ixyFFrlUuSMEUL94n2rz4NrKhJ8z8peRIa6E7hXgweq6ueQb1uWNjdXQw7IWkzGksUWuHu5moSCFekPOkkCVnkQyyQv5ucqfyakdeR6T5Kv6UUG1b_8QmeDxwIcF8su89cEFuK3q8X0ykZf8imq-J9nO0RusrtDFQ4F1_46h0rxhogqCwxZwkF0zK03drxasG5-lJ4M5pcdv8r7yZS5ZJKc2OorZFtiwQkJrmi2rgMj7XSB1wAoULSUmgCJ6ynjPT5lY2vHfioReqJiaRDmx_x1G00__y30000)

### Giải thích biểu đồ lớp:

- Employee: Lớp đại diện cho nhân viên, bao gồm thông tin về ID nhân viên, tên, loại hình thanh toán, lịch trình thanh toán và phương thức thanh toán.

- Payment: Lớp chịu trách nhiệm xử lý thanh toán, lưu trữ thông tin về ID giao dịch, số tiền và ngày thanh toán.

- Timecard: Lớp lưu trữ thông tin chấm công của nhân viên theo giờ, bao gồm ngày làm việc, số giờ làm việc, và mã charge number của dự án liên quan.

- PaymentMethod: Lớp quản lý phương thức thanh toán mà nhân viên lựa chọn, chẳng hạn như chuyển khoản ngân hàng hoặc nhận phiếu lương qua bưu điện.

- ProjectManagement: Lớp chứa thông tin về các dự án và charge number để gán chi phí và giờ làm việc vào các dự án cụ thể.

## 4. Mối quan hệ giữa các lớp

- Employee có quan hệ hai chiều với Payment: Nhân viên có thể nhận nhiều khoản thanh toán trong các kỳ thanh toán khác nhau.

- Employee cũng có quan hệ với Timecard: Thông tin chấm công được nhân viên cung cấp để tính toán lương.

- Payment tương tác với PaymentMethod để xác định cách thức thanh toán cho từng nhân viên.

- Timecard liên kết với ProjectManagement để xác định chi phí và giờ làm việc cho từng dự án của nhân viên.


# Phân tích ca sử dụng Maintain Timecard

Trong phần này, em sẽ phân tích ca sử dụng (Use Case) "Maintain Timecard" nhằm hiểu rõ các lớp liên quan, hành vi của hệ thống thông qua biểu đồ sequence, và xác định các nhiệm vụ, thuộc tính, cũng như mối quan hệ giữa các lớp phân tích.

## 1. Xác định các lớp phân tích cho ca sử dụng Maintain Timecard

Ca sử dụng "Maintain Timecard" chịu trách nhiệm quản lý thông tin chấm công cho nhân viên. Dưới đây là các lớp phân tích chính trong ca sử dụng này:

### 1.1 Lớp `Employee`

- **Nhiệm vụ**: Đại diện cho nhân viên trong hệ thống, lưu trữ và quản lý thông tin cá nhân và chấm công.

- **Thuộc tính**:

  - `employeeID`: Mã số nhân viên.

  - `name`: Tên nhân viên.

  - `timecards`: Danh sách các phiếu chấm công đã ghi nhận.

### 1.2 Lớp `Timecard`

- **Nhiệm vụ**: Quản lý thông tin chấm công của nhân viên làm việc theo giờ. Phiếu chấm công ghi nhận ngày làm việc, số giờ làm việc, và mã charge number liên quan.

- **Thuộc tính**:

  - `timecardID`: Mã chấm công.

  - `date`: Ngày làm việc.

  - `hoursWorked`: Số giờ làm việc.

  - `chargeNumber`: Mã charge number của dự án.

### 1.3 Lớp `ProjectManagement`

- **Nhiệm vụ**: Lấy thông tin về dự án và số charge number để gán giờ làm việc của nhân viên vào từng dự án.

- **Thuộc tính**:

  - `projectID`: Mã dự án.

  - `chargeNumber`: Mã charge number.

### 1.4 Lớp `TimecardAdministrator`

- **Nhiệm vụ**: Quản trị viên chịu trách nhiệm duy trì và quản lý các phiếu chấm công, đảm bảo rằng thông tin được ghi nhận đầy đủ và chính xác.

- **Thuộc tính**:

  - `adminID`: Mã quản trị viên.

## 2. Biểu đồ Sequence cho ca sử dụng Maintain Timecard

Biểu đồ sequence dưới đây mô tả luồng hoạt động khi hệ thống thực hiện chức năng duy trì phiếu chấm công:

![Diagram](https://www.planttext.com/api/plantuml/png/R96z3S8m48LxJt4B8FeKY2YA40K81HZWY1zWXEtWN92OZOAHM86a2C50--vxFvQVzyUq5WxIsBFYKdoWZR4eEUXKM-DCBO5RLLKjOqfJiHFARNNsDo0IUriahe8_ePG5Epx0mebIV-DfD7cd9bJWqg0U8cdkzbxrzuxjBmcbMezpRJxwtwwM--bFQ0QXxCZX05esTeUWVY0QHHK5f0dkopIqHDFNVCKmPPZy4HWzFA5jfLb0cMzP2DGKJdUVyG800F__0m00)

### Giải thích biểu đồ Sequence:

- TimecardAdministrator yêu cầu thông tin chấm công của nhân viên.

- Employee có thể thêm hoặc chỉnh sửa phiếu chấm công dựa trên giờ làm việc thực tế.

- Timecard tương tác với ProjectManagement để lấy mã charge number tương ứng với dự án mà nhân viên đã làm việc.

- Timecard ghi nhận và lưu lại phiếu chấm công đã chỉnh sửa.

- Sau khi hoàn tất, Employee thông báo cho TimecardAdministrator rằng việc cập nhật chấm công đã hoàn thành.

## 3. Biểu đồ lớp phân tích (Class Diagram)

![Diagram](https://www.planttext.com/api/plantuml/png/X971YW8n343l_OemnuKHzxg8AEXXONTPMC5pd8QnEcqbpHmMySiy-4d-WfsnKv4zx2daXRoawVLycGL1bjOsgcem15ZQG-D_YU2e04gWbBulu0sCanuwj1JJ7s7Zwfw8iLGXwn3nXmaoMIKmLIULp0DAvg7boQnHElCYXZxV-fR3slEUTCJQjvlcNgYso3LzjNP3_5Wbp_fclwDAFj5XJPQSfA67Et-Q-OzgM7kkhN7nQOpYEUcmOraMM_BrYjS2oXAAyMZqKcI7oZSOwZ7ysLMf6JdTVSaD003__mC0)

### Giải thích biểu đồ lớp:

- Employee: Lớp đại diện cho nhân viên, quản lý danh sách các phiếu chấm công mà nhân viên đã ghi nhận.

- Timecard: Lớp chứa thông tin về phiếu chấm công, bao gồm ngày làm việc, số giờ đã làm, và mã charge number của dự án liên quan.

- ProjectManagement: Lớp quản lý thông tin về dự án và mã charge number, phục vụ cho việc gán giờ làm việc của nhân viên vào dự án cụ thể.

- TimecardAdministrator: Quản trị viên có trách nhiệm duy trì và quản lý các phiếu chấm công.

## 4. Mối quan hệ giữa các lớp

- Employee có quan hệ một-nhiều với Timecard: Mỗi nhân viên có thể có nhiều phiếu chấm công tương ứng với các ngày làm việc khác nhau.

- Timecard tương tác với ProjectManagement để lấy thông tin mã charge number của dự án.

- TimecardAdministrator có vai trò quản lý toàn bộ quy trình chấm công và phiếu chấm công của nhân viên.