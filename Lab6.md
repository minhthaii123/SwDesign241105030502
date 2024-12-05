# LAB 6: 
## code (
@startuml
' Sơ đồ Class cho Payroll System với Operations và Methods

' 1. BankSystem
package "BankSystem" {
    class IBankSystem {
        +deposit(aPaycheck: Paycheck, intoBank: BankInformation)
    }

    class BankSystem {
        +processTransaction(transactionID: String)
        +getTransactionStatus(transactionID: String): TransactionStatus
    }

    class Paycheck {
        - employeeID: String
        - amount: Double
        - date: Date
    }

    class BankInformation {
        - accountNumber: String
        - bankName: String
        - branchCode: String
    }
}

' 2. PrintService
package "PrintService" {
    class IPrintService {
        +printPaySlip(aPaycheck: Paycheck, employeeInfo: EmployeeInformation)
    }

    class PrintService {
        +generatePaySlip(aPaycheck: Paycheck, templateID: String): PrintedPaySlip
        +generateReport(reportType: String, dateRange: DateRange): Report
    }

    class Paycheck {
        - employeeID: String
        - amount: Double
        - date: Date
    }

    class EmployeeInformation {
        - employeeID: String
        - name: String
        - department: String
    }
}

' 3. ProjectManagementDatabase
package "ProjectManagementDatabase" {
    class IProjectManagementDatabase {
        +fetchProjectData(projectID: int): ProjectInformation
        +getAllProjects(): List<ProjectInformation>
        +fetchEmployeeAssignments(employeeID: int): List<EmployeeAssignment>
    }

    class ProjectManagementDatabase {
        +updateAssignment(employeeID: int, projectID: int, role: String)
    }

    class ProjectInformation {
        - projectID: int
        - projectName: String
        - startDate: Date
        - endDate: Date
    }

    class EmployeeAssignment {
        - employeeID: String
        - projectID: int
        - role: String
    }
}

' 4. PayrollProcessing
package "PayrollProcessing" {
    class PayrollController {
        +generatePaycheck(employeeID: int): Paycheck
        +processTimecard(timecard: Timecard)
        +requestBankTransfer(paycheck: Paycheck)
        +requestPaySlipPrint(paycheck: Paycheck)
    }

    class PayrollCalculator {
        +calculatePay(timecard: Timecard): Paycheck
    }

    class Timecard {
        - hoursWorked: int
        - projectID: int
    }

    class Paycheck {
        - employeeID: String
        - amount: Double
        - date: Date
    }
}

' Quan hệ giữa các lớp
IBankSystem --> BankSystem : "Gửi yêu cầu giao dịch"
BankSystem --> Paycheck : "Truy cập thông tin phiếu lương"
BankSystem --> BankInformation : "Sử dụng thông tin ngân hàng"

PayrollController --> IPrintService : "Gửi yêu cầu in phiếu lương"
IPrintService --> PrintService : "Thực hiện in phiếu lương"
PrintService --> Paycheck : "Sử dụng thông tin phiếu lương"
PrintService --> EmployeeInformation : "Sử dụng thông tin nhân viên"

PayrollController --> IProjectManagementDatabase : "Truy xuất dữ liệu dự án"
IProjectManagementDatabase --> ProjectManagementDatabase : "Lưu trữ và truy xuất dữ liệu"
ProjectManagementDatabase --> ProjectInformation : "Lưu trữ thông tin dự án"
ProjectManagementDatabase --> EmployeeAssignment : "Quản lý phân công nhân viên"

PayrollController --> PayrollCalculator : "Yêu cầu tính toán tiền lương"
PayrollController --> BankSystem : "Gửi yêu cầu chuyển tiền"
PayrollController --> PrintService : "Gửi yêu cầu in phiếu lương"

PayrollCalculator --> Timecard : "Sử dụng thông tin giờ làm việc"
PayrollCalculator --> Paycheck : "Tạo phiếu lương"
@enduml
)
1. BankSystem
Mục tiêu: Xử lý giao dịch gửi tiền trực tiếp vào tài khoản ngân hàng.

Operations và Methods:
Gửi tiền lương vào tài khoản ngân hàng:
IBankSystem.deposit(aPaycheck: Paycheck, intoBank: BankInformation)
Mô tả: Nhận phiếu lương và thông tin ngân hàng, xử lý giao dịch gửi tiền.
BankSystem.processTransaction(transactionID: String)
Mô tả: Thực hiện xác thực và hoàn tất giao dịch.
Kiểm tra trạng thái giao dịch:
BankSystem.getTransactionStatus(transactionID: String): TransactionStatus
Mô tả: Truy vấn trạng thái giao dịch (đang xử lý, hoàn tất, thất bại).
2. PrintService
Mục tiêu: Xử lý việc in phiếu lương và báo cáo lương.

Operations và Methods:
In phiếu lương:
IPrintService.printPaySlip(aPaycheck: Paycheck, employeeInfo: EmployeeInformation)
Mô tả: Nhận phiếu lương và thông tin nhân viên để tạo bản in.
PrintService.generatePaySlip(aPaycheck: Paycheck, templateID: String): PrintedPaySlip
Mô tả: Tạo bản in phiếu lương theo mẫu in định sẵn.
In báo cáo lương:
PrintService.generateReport(reportType: String, dateRange: DateRange): Report
Mô tả: Tạo báo cáo lương dựa trên loại báo cáo và thời gian chỉ định.
3. ProjectManagementDatabase
Mục tiêu: Quản lý thông tin dự án, phân công nhân viên, và dữ liệu công việc.

Operations và Methods:
Truy xuất dữ liệu dự án:

IProjectManagementDatabase.fetchProjectData(projectID: int): ProjectInformation
Mô tả: Lấy thông tin chi tiết của một dự án.
IProjectManagementDatabase.getAllProjects(): List<ProjectInformation>
Mô tả: Lấy danh sách tất cả các dự án.
Phân công và cập nhật nhân viên:

IProjectManagementDatabase.fetchEmployeeAssignments(employeeID: int): List<EmployeeAssignment>
Mô tả: Lấy danh sách phân công của một nhân viên.
ProjectManagementDatabase.updateAssignment(employeeID: int, projectID: int, role: String)
Mô tả: Cập nhật vai trò hoặc dự án cho một nhân viên.
4. PayrollProcessing
Mục tiêu: Tính toán lương và quản lý thông tin thanh toán.

Operations và Methods:
Tính toán lương:

PayrollCalculator.calculatePay(timecard: Timecard): Paycheck
Mô tả: Tính toán phiếu lương dựa trên dữ liệu thời gian làm việc (Timecard).
Tạo phiếu lương:

PayrollController.generatePaycheck(employeeID: int): Paycheck
Mô tả: Tạo phiếu lương cho nhân viên dựa trên ID của họ.
Quản lý thông tin giờ làm việc:

PayrollController.processTimecard(timecard: Timecard)
Mô tả: Xử lý dữ liệu giờ làm việc để chuẩn bị tính toán lương.
Gửi tiền và in phiếu lương:

PayrollController.requestBankTransfer(paycheck: Paycheck)
Mô tả: Gửi yêu cầu chuyển khoản lương tới BankSystem.
PayrollController.requestPaySlipPrint(paycheck: Paycheck)
Mô tả: Gửi yêu cầu in phiếu lương tới PrintService.

## 2 Xác định đúng các trạng thái và mô tả sự thay đổi trạng thái
![](https://www.planttext.com/api/plantuml/png/b5KzRnD14EtzAqPfI91YYOyg1Kf888e4oCA61b6izpPtY-zsJtTh2mjHfOWG1OeeA11I34eJAIAHg7n5YelyF-uNy1UOsVlm-IDAgBmx-zxElRSpux_9vMPiM6JwWT-u0-t92AwEikGhc2WRZvGBnaj74hYdWQSZ3bwM768iIuxmZ6k5E8sh5Xj6slUXFOoD21fuqxqcF6QgbmTWdH3S4xpNm6n6m4gvNm4MGrXiu4C3uCtTjx2-_WYs8u581oF5oaPVCrywThS1UzCCJKU4EfPcTGtnKmmnsaAPZYOeKZfU-eTKIGNlIGz9kU38gQ5iSXs4liZJx4gcmScIpzmZEuwLXrxWBOkifqpwIoZP-CH05_sKI2am14UbfAvALSO-ae7tcz2Af39j4Gqa5pTQIDZMxNryAPWpx6YR0Z-udghf2YKYHE9rRL-6rjCPF5rWLrPiovFP-B8F_kHyGYM3tdeQRG93mfTnAv-UPSatIOHLKro2flq6NsAPzTUMkLMcdV7g0NcbtmbkdZF5N17Wi-mmmxeijiRbPtjgNqS1CrAhoiA5ayBCAdmBAr-5PK5kOpLzmlA8i-ICaPGBI4SAuIM4u5iHz-J0udSA1FHGkw7Y6bCjLeZ_4Va4gqWFXTYAO-agEYn5BfvOaM8XFACr3rknvR8id7Ax0I-yzAU2WKnF5Sw8_Z1B3XJ438l0gQJX0E6BbmHwi7135ni6V4sDWhGi-IBh7jOIJykXl6Z6gOVDSY2XOLmW2p_evX5a2KixYFcyxvSlNstoUIGYkI-jb4vwXczlDAcURO0Aj32FTh5I9EAIxnAKIrRGW77dETDcomaqZulnCiYI4-oWsu-mMfgvpwptLfrzOuDVCyAkUOUE30HdaLE-Gxctxs2ApSm3jFlTG9hS_sezR__ET7A0Ypy_m4-F0omjZ73euSz1W7zNRDxRhH3RVL3OD4-xEfgSPyal3g6Nde935Nv8YYjIJV2cK0xzZVu3003__mC0)

1. BankSystem
Mục tiêu: Xử lý giao dịch gửi tiền.

Trạng thái của Paycheck trong BankSystem:
Created: Phiếu lương được tạo.
Validated: Thông tin phiếu lương được xác thực.
SentToBank: Gửi yêu cầu giao dịch đến ngân hàng.
Completed: Giao dịch được hoàn tất.
Failed: Giao dịch bị lỗi (ví dụ: thông tin ngân hàng sai).
Mô tả sự thay đổi trạng thái:
Created → Validated: Khi phương thức IBankSystem.deposit() được gọi và dữ liệu được kiểm tra.
Validated → SentToBank: Sau khi xác thực thông tin thành công, gửi yêu cầu đến ngân hàng.
SentToBank → Completed: Giao dịch thành công.
SentToBank → Failed: Giao dịch không thành công (nguyên nhân có thể là thông tin ngân hàng không hợp lệ).
2. PrintService
Mục tiêu: Xử lý việc in phiếu lương và báo cáo.

Trạng thái của Paycheck trong PrintService:
Created: Phiếu lương được tạo.
ReadyToPrint: Phiếu lương đã sẵn sàng để in.
Printed: Phiếu lương được in hoàn tất.
Failed: In phiếu lương bị lỗi.
Mô tả sự thay đổi trạng thái:
Created → ReadyToPrint: Khi phương thức PrintService.generatePaySlip() được gọi và dữ liệu đã được chuẩn bị.
ReadyToPrint → Printed: Phiếu lương được in thành công.
ReadyToPrint → Failed: Lỗi trong quá trình in (ví dụ: thiếu dữ liệu).
3. ProjectManagementDatabase
Mục tiêu: Quản lý thông tin dự án và phân công nhân viên.

Trạng thái của ProjectInformation:
Created: Dự án được tạo.
Updated: Dự án được chỉnh sửa.
Archived: Dự án được lưu trữ hoặc kết thúc.
Mô tả sự thay đổi trạng thái:
Created → Updated: Khi thông tin dự án được chỉnh sửa bằng phương thức updateProjectData().
Updated → Archived: Khi dự án kết thúc hoặc không còn hoạt động.
Trạng thái của EmployeeAssignment:
Assigned: Nhân viên được phân công vào dự án.
Reassigned: Nhân viên được phân công lại sang dự án khác.
Removed: Nhân viên bị loại khỏi dự án.
Mô tả sự thay đổi trạng thái:
Assigned → Reassigned: Khi thay đổi nhiệm vụ hoặc dự án của nhân viên.
Assigned → Removed: Khi nhân viên không còn tham gia dự án.
4. PayrollProcessing
Mục tiêu: Tính toán lương và quản lý phiếu lương.

Trạng thái của Paycheck:
Calculated: Phiếu lương được tính toán.
Verified: Phiếu lương được xác minh.
SentToBank: Phiếu lương được gửi đến ngân hàng.
Printed: Phiếu lương được in.
Completed: Quy trình xử lý lương hoàn tất.
Mô tả sự thay đổi trạng thái:
Calculated → Verified: Khi phương thức PayrollCalculator.calculatePay() hoàn thành tính toán.
Verified → SentToBank: Khi phiếu lương được gửi đến BankSystem.
Verified → Printed: Khi phiếu lương được gửi đến PrintService để in.
SentToBank/Printed → Completed: Quy trình xử lý lương kết thúc.
Trạng thái của Timecard:
Submitted: Thông tin giờ làm việc được nhập vào hệ thống.
Verified: Thông tin giờ làm việc được xác minh.
Approved: Thông tin giờ làm việc được chấp thuận cho tính lương.
Mô tả sự thay đổi trạng thái:
Submitted → Verified: Khi dữ liệu giờ làm việc được kiểm tra.
Verified → Approved: Khi thông tin được chấp thuận và sẵn sàng để tính lương.

##  3 Xác định đúng các thuộc tính và mô tả rõ ràng
![](https://www.planttext.com/api/plantuml/png/t5QzZjD04Exz5ACqG94NI7K_GIBISJem4lLclTZ6zgvbhoD5AFNLY9A68D4WeGE92XTN6EKz_0Iymirk76VjU1FgS-6VcTblvfjlTfD_vVrPBaacYoHsde2xMSFVZtNv2IvZakT00m4tP9c9E0PtcKkME1XrGNZKVAM4HiHdCDhRHl310RoeHi3LD60qQepg6WDBqbWi6PjD9-3ABEI-uII9ABYSm5GKyvWP3ez8XcQyjqO0dyddBThJPmTuEk9SGofl3rHx5QBsxP1NZa504PlnTo9BY0m5x_0Wb2hWwoAPiso0oXpNNfE43RaomcbmARn3vxPa4zh6wwB1j_hR9Bs8bRDIGjwWGReiMuIKxQKqhOzCp1RT8kXHBdnOIO-bk7yIfcWErNkQqJ49foswJKBndb7vad3KJeKXSJ8dUKTFIqXFt6sOhJLfuyREu7WSEYnphW-NwQ7Os6lk3TWrwLqfkcDcDjDxh6lkBcjd5FQIR5EVdfFpF0zzhdhs_sDYRHIUefRDVdf4ZdVaDI9RncDxUEDoof0BElTZqNSziht-9amO9PdN8H288ilVYYnYdcME-xhfJ2_souwDP5UUHe9N1U4GrEKj-65TtX6WrPf2N9UVKwTjydXyy4CpWP5Rbp_0gyjlt0SPLB_L8-J0_UehGbPVKBCEnD3nXZ0p3caGrd_k2uWtFpVh_hA1dTzBZeyxYB7ysqAz_u9gpOTJ6pi6CQx2wZk725DBM23Z40jHjLFDXUltXOePEQrSreAcHX4oOCAen3d3qqJzXNa0003__mC0)

1. BankSystem
Lớp Paycheck:
employeeID (String): Mã định danh của nhân viên nhận lương.
Mô tả: Xác định phiếu lương thuộc về nhân viên nào.
amount (Double): Số tiền trong phiếu lương.
Mô tả: Tổng số tiền mà nhân viên sẽ nhận.
date (Date): Ngày tạo phiếu lương.
Mô tả: Lưu ngày mà phiếu lương được tính toán hoặc gửi.
Lớp BankInformation:
accountNumber (String): Số tài khoản ngân hàng của nhân viên.
Mô tả: Tài khoản mà lương sẽ được gửi vào.
bankName (String): Tên ngân hàng.
Mô tả: Ngân hàng nơi tài khoản được mở.
branchCode (String): Mã chi nhánh ngân hàng.
Mô tả: Xác định chi nhánh liên quan.
2. PrintService
Lớp Paycheck (kế thừa từ BankSystem):
employeeID (String): Mã định danh của nhân viên.
Mô tả: Thông tin cần thiết để in phiếu lương.
amount (Double): Số tiền lương.
Mô tả: Hiển thị trên phiếu lương.
date (Date): Ngày lương được trả.
Mô tả: Hiển thị thông tin ngày in phiếu lương.
Lớp EmployeeInformation:
employeeID (String): Mã nhân viên.
Mô tả: Xác định nhân viên để in phiếu lương.
name (String): Tên nhân viên.
Mô tả: Hiển thị trên phiếu lương hoặc báo cáo.
department (String): Bộ phận mà nhân viên làm việc.
Mô tả: Phân loại nhân viên theo đơn vị công tác.
3. ProjectManagementDatabase
Lớp ProjectInformation:
projectID (int): Mã định danh dự án.
Mô tả: Dự án mà nhân viên tham gia.
projectName (String): Tên dự án.
Mô tả: Nhận diện dự án trong cơ sở dữ liệu.
startDate (Date): Ngày bắt đầu dự án.
Mô tả: Theo dõi thời gian thực hiện dự án.
endDate (Date): Ngày kết thúc dự án.
Mô tả: Theo dõi thời hạn dự án.
Lớp EmployeeAssignment:
employeeID (String): Mã nhân viên.
Mô tả: Gán nhân viên vào dự án.
projectID (int): Mã dự án.
Mô tả: Dự án mà nhân viên được phân công.
role (String): Vai trò của nhân viên trong dự án.
Mô tả: Xác định trách nhiệm cụ thể của nhân viên.
4. PayrollProcessing
Lớp Paycheck:
employeeID (String): Mã định danh của nhân viên.
Mô tả: Phiếu lương được gán cho nhân viên này.
amount (Double): Tổng số tiền lương.
Mô tả: Số tiền sau khi tính toán từ giờ làm việc và các khoản phụ cấp.
date (Date): Ngày tính lương.
Mô tả: Ghi lại thời điểm lương được xử lý.
Lớp Timecard:
hoursWorked (int): Số giờ làm việc của nhân viên.
Mô tả: Dữ liệu dùng để tính lương.
projectID (int): Mã dự án mà giờ làm việc thuộc về.
Mô tả: Phân loại giờ làm việc theo từng dự án.

## 4 Xác định đúng các phụ thuộc và quan hệ kết hợp
1. BankSystem
Phụ thuộc:
PayrollController → IBankSystem

Loại: Dependency
Mô tả: PayrollController phụ thuộc vào IBankSystem để gửi yêu cầu giao dịch tiền lương.
Cách sử dụng: Gọi phương thức IBankSystem.deposit(aPaycheck, intoBank).
IBankSystem → BankSystem

Loại: Dependency
Mô tả: IBankSystem phụ thuộc vào BankSystem để thực hiện xử lý giao dịch thực tế.
Quan hệ kết hợp:
BankSystem → Paycheck

Loại: Association
Mô tả: BankSystem liên kết với Paycheck để truy cập thông tin lương của nhân viên.
BankSystem → BankInformation

Loại: Association
Mô tả: BankSystem sử dụng thông tin từ BankInformation để thực hiện giao dịch.
2. PrintService
Phụ thuộc:
PayrollController → IPrintService

Loại: Dependency
Mô tả: PayrollController phụ thuộc vào IPrintService để gửi yêu cầu in phiếu lương.
Cách sử dụng: Gọi phương thức IPrintService.printPaySlip(aPaycheck, employeeInfo).
IPrintService → PrintService

Loại: Dependency
Mô tả: IPrintService phụ thuộc vào PrintService để thực hiện lệnh in.
Quan hệ kết hợp:
PrintService → Paycheck

Loại: Association
Mô tả: PrintService liên kết với Paycheck để sử dụng thông tin phiếu lương trong quá trình in.
PrintService → EmployeeInformation

Loại: Association
Mô tả: PrintService sử dụng thông tin nhân viên từ EmployeeInformation để tạo phiếu lương đúng.
3. ProjectManagementDatabase
Phụ thuộc:
PayrollController → IProjectManagementDatabase

Loại: Dependency
Mô tả: PayrollController phụ thuộc vào IProjectManagementDatabase để truy xuất dữ liệu về dự án và nhân viên.
Cách sử dụng: Gọi phương thức fetchProjectData(projectID) hoặc fetchEmployeeAssignments(employeeID).
IProjectManagementDatabase → ProjectManagementDatabase

Loại: Dependency
Mô tả: IProjectManagementDatabase phụ thuộc vào ProjectManagementDatabase để xử lý dữ liệu thực tế.
Quan hệ kết hợp:
ProjectManagementDatabase → ProjectInformation

Loại: Association
Mô tả: ProjectManagementDatabase liên kết với ProjectInformation để lưu trữ thông tin chi tiết về dự án.
ProjectManagementDatabase → EmployeeAssignment

Loại: Association
Mô tả: ProjectManagementDatabase sử dụng EmployeeAssignment để quản lý phân công nhân viên trong dự án.
4. PayrollProcessing
Phụ thuộc:
PayrollController → PayrollCalculator

Loại: Dependency
Mô tả: PayrollController phụ thuộc vào PayrollCalculator để tính toán phiếu lương.
Cách sử dụng: Gọi phương thức PayrollCalculator.calculatePay(timecard).
PayrollController → PrintService

Loại: Dependency
Mô tả: PayrollController gửi yêu cầu in phiếu lương đến PrintService.
PayrollController → BankSystem

Loại: Dependency
Mô tả: PayrollController gửi yêu cầu chuyển tiền đến BankSystem.
Quan hệ kết hợp:
PayrollCalculator → Timecard

Loại: Association
Mô tả: PayrollCalculator sử dụng thông tin từ Timecard để tính toán tiền lương.
PayrollCalculator → Paycheck

Loại: Association
Mô tả: PayrollCalculator tạo Paycheck sau khi tính toán lương.
## CODE (@startuml
' Sơ đồ mô tả các hệ thống con trong Payroll System

' BankSystem
package "BankSystem" {
    class IBankSystem {
        +deposit(aPaycheck: Paycheck, intoBank: BankInformation)
    }

    class BankSystem {
        +processTransaction(transactionID: String)
        +getTransactionStatus(transactionID: String): TransactionStatus
    }

    class Paycheck
    class BankInformation
}

' Phụ thuộc và quan hệ kết hợp BankSystem
PayrollController --> IBankSystem : "Gửi yêu cầu giao dịch"
IBankSystem --> BankSystem : "Thực hiện giao dịch"
BankSystem --> Paycheck : "Truy cập thông tin phiếu lương"
BankSystem --> BankInformation : "Sử dụng thông tin ngân hàng"

' PrintService
package "PrintService" {
    class IPrintService {
        +printPaySlip(aPaycheck: Paycheck, employeeInfo: EmployeeInformation)
    }

    class PrintService {
        +generatePaySlip(aPaycheck: Paycheck, templateID: String): PrintedPaySlip
    }

    class Paycheck
    class EmployeeInformation
}

' Phụ thuộc và quan hệ kết hợp PrintService
PayrollController --> IPrintService : "Gửi yêu cầu in phiếu lương"
IPrintService --> PrintService : "Thực hiện in phiếu lương"
PrintService --> Paycheck : "Sử dụng thông tin phiếu lương"
PrintService --> EmployeeInformation : "Sử dụng thông tin nhân viên"

' ProjectManagementDatabase
package "ProjectManagementDatabase" {
    class IProjectManagementDatabase {
        +fetchProjectData(projectID: int): ProjectInformation
        +fetchEmployeeAssignments(employeeID: int): List<EmployeeAssignment>
    }

    class ProjectManagementDatabase {
        +storeData()
    }

    class ProjectInformation
    class EmployeeAssignment
}

' Phụ thuộc và quan hệ kết hợp ProjectManagementDatabase
PayrollController --> IProjectManagementDatabase : "Truy xuất dữ liệu dự án"
IProjectManagementDatabase --> ProjectManagementDatabase : "Lưu trữ và truy xuất dữ liệu"
ProjectManagementDatabase --> ProjectInformation : "Lưu trữ thông tin dự án"
ProjectManagementDatabase --> EmployeeAssignment : "Quản lý phân công nhân viên"

' PayrollProcessing
package "PayrollProcessing" {
    class PayrollController {
        +calculatePayroll()
        +generatePaycheck(employeeID: int): Paycheck
        +requestBankTransfer(paycheck: Paycheck)
        +requestPaySlipPrint(paycheck: Paycheck)
    }

    class PayrollCalculator {
        +calculatePay(timecard: Timecard): Paycheck
    }

    class Timecard
    class Paycheck
}

' Phụ thuộc và quan hệ kết hợp PayrollProcessing
PayrollController --> PayrollCalculator : "Yêu cầu tính toán tiền lương"
PayrollController --> PrintService : "Gửi yêu cầu in phiếu lương"
PayrollController --> BankSystem : "Gửi yêu cầu chuyển tiền"
PayrollCalculator --> Timecard : "Sử dụng thông tin giờ làm việc"
PayrollCalculator --> Paycheck : "Tạo phiếu lương"

@enduml
)
