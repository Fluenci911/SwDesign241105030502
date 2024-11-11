# Phân tích các ca sử dụng trong hệ thống Payroll System

## 1. Ca sử dụng "Record Timecard"

**Mô tả**: Cho phép nhân viên ghi nhận giờ làm việc của mình.

- **Lớp phân tích chính**:
  - `Employee`: Quản lý thông tin nhân viên và danh sách các phiếu chấm công.
  - `Timecard`: Chứa thông tin chấm công của nhân viên, bao gồm ngày làm và số giờ làm.
  - `TimecardAdministrator`: Quản lý và lưu trữ phiếu chấm công.

- **Hành vi (Sequence)**:
  - Nhân viên truy cập hệ thống và nhập dữ liệu chấm công vào lớp `Timecard`.
  - `Timecard` lưu trữ và cập nhật thông tin.
  - `TimecardAdministrator` xác nhận và lưu trữ thông tin chấm công của nhân viên.

## 2. Ca sử dụng "Calculate Payment"

**Mô tả**: Tính toán lương cho nhân viên dựa trên loại hình công việc (giờ làm việc, lương cố định, hoặc có hoa hồng).

- **Lớp phân tích chính**:
  - `Employee`: Cung cấp thông tin nhân viên, bao gồm loại hình lương và hoa hồng (nếu có).
  - `Payment`: Tính toán tổng lương dựa trên giờ làm và mức lương của từng nhân viên.
  - `Timecard`: Sử dụng thông tin giờ làm để tính toán lương cho nhân viên làm theo giờ.
  - `Commission`: Lưu thông tin về hoa hồng cho nhân viên bán hàng.

- **Hành vi (Sequence)**:
  - Hệ thống lấy dữ liệu từ `Employee`, `Timecard` và `Commission`.
  - `Payment` thực hiện tính toán lương và hoa hồng (nếu có).
  - Kết quả được lưu trữ trong `Payment` và thông báo tới nhân viên.

## 3. Ca sử dụng "Process Payroll"

**Mô tả**: Tự động xử lý và phát lương định kỳ (thứ 6 hàng tuần hoặc cuối tháng).

- **Lớp phân tích chính**:
  - `Employee`: Cung cấp thông tin nhân viên cần trả lương.
  - `Payment`: Xử lý tổng lương cho từng nhân viên dựa trên các thông tin từ `Timecard` và `Commission`.
  - `PaymentMethod`: Chọn phương thức thanh toán (chuyển khoản, nhận tiền mặt, hoặc gửi qua bưu điện).

- **Hành vi (Sequence)**:
  - `Payment` truy vấn từ các lớp liên quan để tính tổng số tiền lương.
  - `PaymentMethod` xác định phương thức thanh toán.
  - Lương được phát hành tự động dựa trên phương thức thanh toán mà nhân viên chọn.

## 4. Ca sử dụng "Generate Reports"

**Mô tả**: Hỗ trợ nhân viên và quản trị viên tạo các báo cáo về giờ làm việc, lương, và thông tin dự án.

- **Lớp phân tích chính**:
  - `Employee`: Cung cấp dữ liệu nhân viên và thông tin lương để lập báo cáo.
  - `Timecard`: Cung cấp chi tiết chấm công của nhân viên.
  - `ProjectManagement`: Cung cấp thông tin về dự án và charge number.

- **Hành vi (Sequence)**:
  - Hệ thống truy vấn thông tin từ các lớp `Employee`, `Timecard`, và `ProjectManagement`.
  - Dữ liệu được tổng hợp và xử lý để xuất thành báo cáo.

## 5. Ca sử dụng "Maintain Employee Information"

**Mô tả**: Hỗ trợ quản trị viên cập nhật, thêm mới, hoặc xóa thông tin nhân viên trong hệ thống.

- **Lớp phân tích chính**:
  - `Employee`: Chứa thông tin của nhân viên, bao gồm ID, tên, phương thức thanh toán, và loại hình lương.
  - `PayrollAdministrator`: Quản lý việc cập nhật thông tin nhân viên và thực hiện các thay đổi cần thiết.

- **Hành vi (Sequence)**:
  - `PayrollAdministrator` yêu cầu các thay đổi (thêm, sửa, hoặc xóa) thông tin của `Employee`.
  - Hệ thống cập nhật cơ sở dữ liệu và lưu thông tin mới.

## 6. Ca sử dụng "Update Payment Method"

**Mô tả**: Cho phép nhân viên thay đổi phương thức nhận lương của mình.

- **Lớp phân tích chính**:
  - `Employee`: Chứa thông tin cá nhân của nhân viên và lựa chọn phương thức thanh toán.
  - `PaymentMethod`: Quản lý các phương thức thanh toán, bao gồm chuyển khoản, nhận tiền mặt, hoặc gửi qua bưu điện.

- **Hành vi (Sequence)**:
  - Nhân viên truy cập vào hệ thống và cập nhật lựa chọn của mình trong `PaymentMethod`.
  - `PaymentMethod` xác nhận và lưu lựa chọn mới của nhân viên.

---

## Tổng kết

Phân tích các ca sử dụng trong hệ thống Payroll System cho phép xác định rõ ràng từng chức năng và các lớp liên quan. Các lớp `Employee`, `Timecard`, `Payment`, `PaymentMethod`, `Commission`, `ProjectManagement`, và `PayrollAdministrator` đều đóng vai trò quan trọng trong từng quy trình và tạo thành một hệ thống hoàn chỉnh, đảm bảo tính tự động, chính xác, và bảo mật trong việc xử lý chấm công và phát lương cho nhân viên.

# Bài code cho hệ thống Payroll System

Bài code dưới đây mô phỏng một phần của hệ thống Payroll System với chức năng "Maintain Timecard", cho phép cập nhật và quản lý phiếu chấm công cho nhân viên.

## Bài Code

```java
package Lab2;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

// Lớp Timecard lưu trữ thông tin chấm công của nhân viên
class Timecard {
    private int timecardID;
    private Date date;
    private double hoursWorked;
    private String chargeNumber;

    public Timecard(int timecardID, Date date, double hoursWorked, String chargeNumber) {
        this.timecardID = timecardID;
        this.date = date;
        this.hoursWorked = hoursWorked;
        this.chargeNumber = chargeNumber;
    }

    // Getter và Setter cho các thuộc tính
    public int getTimecardID() {
        return timecardID;
    }

    public Date getDate() {
        return date;
    }

    public double getHoursWorked() {
        return hoursWorked;
    }

    public String getChargeNumber() {
        return chargeNumber;
    }

    public void setHoursWorked(double hoursWorked) {
        this.hoursWorked = hoursWorked;
    }

    @Override
    public String toString() {
        return "Timecard{" +
                "timecardID=" + timecardID +
                ", date=" + date +
                ", hoursWorked=" + hoursWorked +
                ", chargeNumber='" + chargeNumber + '\'' +
                '}';
    }
}

// Lớp Employee quản lý thông tin nhân viên và danh sách các phiếu chấm công
class Employee {
    private int employeeID;
    private String name;
    private List<Timecard> timecards;

    public Employee(int employeeID, String name) {
        this.employeeID = employeeID;
        this.name = name;
        this.timecards = new ArrayList<>();
    }

    // Thêm phiếu chấm công mới
    public void addTimecard(Timecard timecard) {
        timecards.add(timecard);
    }

    // Lấy danh sách phiếu chấm công của nhân viên
    public List<Timecard> getTimecards() {
        return timecards;
    }

    public int getEmployeeID() {
        return employeeID;
    }

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "employeeID=" + employeeID +
                ", name='" + name + '\'' +
                ", timecards=" + timecards +
                '}';
    }
}

// Lớp ProjectManagement quản lý các dự án và charge number
class ProjectManagement {
    public static String getChargeNumber(int projectID) {
        // Giả lập lấy mã số dự án dựa trên ID dự án
        return "CN-" + projectID;
    }
}

// Lớp TimecardAdministrator chịu trách nhiệm cập nhật phiếu chấm công cho nhân viên
class TimecardAdministrator {
    public void maintainTimecard(Employee employee, int timecardID, Date date, double hoursWorked, int projectID) {
        String chargeNumber = ProjectManagement.getChargeNumber(projectID);
        Timecard timecard = new Timecard(timecardID, date, hoursWorked, chargeNumber);
        employee.addTimecard(timecard);
        System.out.println("Timecard updated successfully for employee: " + employee.getName());
    }
}

// Main class để thực thi và kiểm tra ca sử dụng "Maintain Timecard"
public class PayrollSystem {
    public static void main(String[] args) {
        // Tạo một nhân viên
        Employee employee = new Employee(1, "John Doe");

        // Tạo đối tượng quản trị viên chấm công
        TimecardAdministrator administrator = new TimecardAdministrator();

        // Cập nhật phiếu chấm công cho nhân viên
        administrator.maintainTimecard(employee, 101, new Date(), 8.0, 1234);

        // In danh sách phiếu chấm công
        System.out.println(employee);
    }
}
```
### Giải thích code
Hệ thống Payroll System dưới đây bao gồm các lớp để quản lý thông tin nhân viên và phiếu chấm công của họ. Các lớp này mô phỏng quy trình "Maintain Timecard" (duy trì phiếu chấm công), cho phép cập nhật và quản lý các phiếu chấm công của nhân viên.

## 1. Lớp `Timecard`

- **Chức năng**: Lớp này đại diện cho phiếu chấm công của nhân viên, chứa các thông tin như:
  - `timecardID`: ID của phiếu chấm công.
  - `date`: Ngày làm việc.
  - `hoursWorked`: Số giờ làm việc.
  - `chargeNumber`: Mã dự án.
  
- **Phương thức**:
  - **Constructor**: Khởi tạo đối tượng `Timecard` với các thuộc tính cơ bản (`timecardID`, `date`, `hoursWorked`, `chargeNumber`).
  - **Getter và Setter**: Cung cấp phương thức để lấy hoặc cập nhật thông tin cho các thuộc tính.
  - **toString()**: Ghi đè phương thức `toString()` để trả về thông tin chi tiết của phiếu chấm công.

## 2. Lớp `Employee`

- **Chức năng**: Lớp này quản lý thông tin của nhân viên, bao gồm:
  - `employeeID`: ID của nhân viên.
  - `name`: Tên của nhân viên.
  - `timecards`: Danh sách các phiếu chấm công của nhân viên.
  
- **Phương thức**:
  - **Constructor**: Khởi tạo đối tượng `Employee` với `employeeID` và `name`, đồng thời khởi tạo một danh sách rỗng cho các phiếu chấm công (`timecards`).
  - **addTimecard(Timecard timecard)**: Thêm một phiếu chấm công mới vào danh sách `timecards`.
  - **getTimecards()**: Trả về danh sách phiếu chấm công của nhân viên.
  - **toString()**: Ghi đè phương thức `toString()` để trả về thông tin chi tiết của nhân viên, bao gồm các phiếu chấm công.

## 3. Lớp `ProjectManagement`

- **Chức năng**: Lớp này mô phỏng quản lý dự án và cung cấp mã số dự án (`chargeNumber`) dựa trên `projectID`.
  
- **Phương thức**:
  - **getChargeNumber(int projectID)**: Phương thức tĩnh, trả về mã số dự án dưới dạng chuỗi dựa trên `projectID`.

## 4. Lớp `TimecardAdministrator`

- **Chức năng**: Lớp này chịu trách nhiệm quản lý phiếu chấm công cho nhân viên.
  
- **Phương thức**:
  - **maintainTimecard(Employee employee, int timecardID, Date date, double hoursWorked, int projectID)**: Tạo phiếu chấm công mới dựa trên các thông tin đầu vào và thêm nó vào danh sách phiếu chấm công của `Employee`. `chargeNumber` được lấy từ lớp `ProjectManagement` dựa vào `projectID`.

## 5. Lớp `PayrollSystem` (Main class)

- **Chức năng**: Lớp chính này có chứa phương thức `main`, dùng để kiểm tra chức năng của hệ thống.
  
- **Các bước thực hiện trong `main`**:
  - Tạo một đối tượng `Employee`.
  - Tạo một đối tượng `TimecardAdministrator`.
  - Sử dụng `TimecardAdministrator` để thêm phiếu chấm công mới cho nhân viên.
  - In thông tin nhân viên cùng danh sách phiếu chấm công của họ.

## Kết quả đầu ra dự kiến

Sau khi thực thi chương trình, đầu ra sẽ hiển thị thông tin của nhân viên cùng với phiếu chấm công mới được thêm vào. Thông báo cũng sẽ cho biết rằng phiếu chấm công đã được cập nhật thành công.

### Chạy code
Timecard updated successfully for employee: John Doe Employee{employeeID=1, name='John Doe', timecards=[Timecard{timecardID=101, date=Mon Nov 05 00:00:00 GMT 2024, hoursWorked=8.0, chargeNumber='CN-1234'}]}


