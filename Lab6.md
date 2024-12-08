# LAB 6: Thiết kế các lớp dựa vào kết quả thiết kế ca sử dụng ở bài lab trước
## 1 Xác định operations và methods hệ thống con
### 1.1 BankSystem
Mục tiêu: Xử lý giao dịch gửi tiền trực tiếp vào tài khoản ngân hàng.
- **Operations và Methods:**
    - **Gửi tiền lương vào tài khoản ngân hàng:**
        - IBankSystem.deposit(aPaycheck: Paycheck, intoBank: BankInformation)
            - Mô tả: Nhận phiếu lương và thông tin ngân hàng, xử lý giao dịch gửi tiền.
        - BankSystem.processTransaction(transactionID: String)
            - Mô tả: Thực hiện xác thực và hoàn tất giao dịch.
    - **Kiểm tra trạng thái giao dịch:**
        - BankSystem.getTransactionStatus(transactionID: String): TransactionStatus
            - Mô tả: Truy vấn trạng thái giao dịch (đang xử lý, hoàn tất, thất bại).
### 1.2. PrintService
Mục tiêu: Xử lý việc in phiếu lương và báo cáo lương.
- **Operations và Methods:**
- **In phiếu lương:**
    - IPrintService.printPaySlip(aPaycheck: Paycheck, employeeInfo: EmployeeInformation)
        - Mô tả: Nhận phiếu lương và thông tin nhân viên để tạo bản in.
    - PrintService.generatePaySlip(aPaycheck: Paycheck, templateID: String): PrintedPaySlip
        - Mô tả: Tạo bản in phiếu lương theo mẫu in định sẵn.
- **In báo cáo lương:**
    - PrintService.generateReport(reportType: String, dateRange: DateRange): Report
        - Mô tả: Tạo báo cáo lương dựa trên loại báo cáo và thời gian chỉ định.

### 1.3. ProjectManagementDatabase
Mục tiêu: Quản lý thông tin dự án, phân công nhân viên, và dữ liệu công việc.
- **Operations và Methods:**
    - Truy xuất dữ liệu dự án:
        - IProjectManagementDatabase.fetchProjectData(projectID: int): ProjectInformation
            - Mô tả: Lấy thông tin chi tiết của một dự án.
        - IProjectManagementDatabase.getAllProjects(): List<ProjectInformation>
            - Mô tả: Lấy danh sách tất cả các dự án.
- **Phân công và cập nhật nhân viên:**
    - IProjectManagementDatabase.fetchEmployeeAssignments(employeeID: int): List<EmployeeAssignment>
        - Mô tả: Lấy danh sách phân công của một nhân viên.
    - ProjectManagementDatabase.updateAssignment(employeeID: int, projectID: int, role: String)
        - Mô tả: Cập nhật vai trò hoặc dự án cho một nhân viên.

### 1.4. PayrollProcessing
Mục tiêu: Tính toán lương và quản lý thông tin thanh toán.
- **Operations và Methods:**
    - **Tính toán lương:**
        - PayrollCalculator.calculatePay(timecard: Timecard): Paycheck
            - Mô tả: Tính toán phiếu lương dựa trên dữ liệu thời gian làm việc (Timecard).
    - **Tạo phiếu lương:**
        - PayrollController.generatePaycheck(employeeID: int): Paycheck
            - Mô tả: Tạo phiếu lương cho nhân viên dựa trên ID của họ.
    - **Quản lý thông tin giờ làm việc:**
        - PayrollController.processTimecard(timecard: Timecard)
            - Mô tả: Xử lý dữ liệu giờ làm việc để chuẩn bị tính toán lương.
    - **Gửi tiền và in phiếu lương:**
        - PayrollController.requestBankTransfer(paycheck: Paycheck)
            - Mô tả: Gửi yêu cầu chuyển khoản lương tới BankSystem.
        - PayrollController.requestPaySlipPrint(paycheck: Paycheck)
            - Mô tả: Gửi yêu cầu in phiếu lương tới PrintService.
              
### Sơ Đồ
![](https://www.planttext.com/api/plantuml/png/X5I_RjD06D_z59-oa4hj2tH0XO9G1wGYPs4ypXVVqVETkJyL5kg063em0694I6IeAY55RIUaUEYGAk_X9-0LkC-r4wTEQGR7lhlVd-_xVhg_vVMUTSGudyde4SIB2Tnygyhli2-9jK2vXaDI62qbn8LrB8l2gPklrUoF0xwuhCeVAWMxHE7p4pZkGV6g_199DdRWD1YHSWU9C8mweLKKqPh-u2bHHxUyy242_2KirrQuOL2bdD6ZRS0p1sgiJKOGknMTDEW-E3UQCcj7XYXBQgLXx8nGAO9QpSEmu69cZWLbAs1O2vAn57b7-dcMIrqmjb5-4q_A53F4iJxL9X_wRMZ7Iw98oZAct3FYo1jYbsHZvYXlJk7UCEXjxKApql7KiVG0fS-JuEw9jI9Lk8-Ksr0_UWQRkUzhvV2VcGr5riMrlfhFzL68Z55Yac7xidMxRTWxpwp34TRJ6ZEpR5QdnOq58gcNnEcb1Tgie8SLTSV32URqbISAGWvF8HLLUK60pYSKP0Xj7dMZjxFpk1kcNHYygCgfW6B-smEjPkS-410DILL-fdmGtO6seWWS6LyWP9f3paKrk_OW5vUBYKe7KR-XY5xFuoPjeVfSwwZQnHsQKIZyYa80bgSgSFn7_xxGjFMyzzNip67v5o2Hp-Fx5SmdzxBs9nV8NgzgSlEfuk5c21JW0kL7zL2VrWVKeQBS5-7MQNbM-9KsujkK83eEBSOIpiBbXT7u2NB-AuDZh8qEeZsc4hmF_m400F__0m00)

## 2. Xác định đúng các trạng thái và mô tả sự thay đổi trạng thái
### 2.1. BankSystem
Mục tiêu: Xử lý giao dịch gửi tiền.
- **Trạng thái của Paycheck trong BankSystem:**
    - Created: Phiếu lương được tạo.
    - Validated: Thông tin phiếu lương được xác thực.
    - SentToBank: Gửi yêu cầu giao dịch đến ngân hàng.
    - Completed: Giao dịch được hoàn tất.
    - Failed: Giao dịch bị lỗi (ví dụ: thông tin ngân hàng sai).
- **Mô tả sự thay đổi trạng thái:**
    - Created → Validated: Khi phương thức IBankSystem.deposit() được gọi và dữ liệu được kiểm tra.
    - Validated → SentToBank: Sau khi xác thực thông tin thành công, gửi yêu cầu đến ngân hàng.
    - SentToBank → Completed: Giao dịch thành công.
    - SentToBank → Failed: Giao dịch không thành công (nguyên nhân có thể là thông tin ngân hàng không hợp lệ).
### 2.2. PrintService
Mục tiêu: Xử lý việc in phiếu lương và báo cáo.
- **Trạng thái của Paycheck trong PrintService:**
    - Created: Phiếu lương được tạo.
    - ReadyToPrint: Phiếu lương đã sẵn sàng để in.
    - Printed: Phiếu lương được in hoàn tất.
    - Failed: In phiếu lương bị lỗi.
- **Mô tả sự thay đổi trạng thái:**
    - Created → ReadyToPrint: Khi phương thức PrintService.generatePaySlip() được gọi và dữ liệu đã được chuẩn bị.
    - ReadyToPrint → Printed: Phiếu lương được in thành công.
    - ReadyToPrint → Failed: Lỗi trong quá trình in (ví dụ: thiếu dữ liệu).

### 2.3. ProjectManagementDatabase
Mục tiêu: Quản lý thông tin dự án và phân công nhân viên.
- **Trạng thái của ProjectInformation:**
    - Created: Dự án được tạo.
    - Updated: Dự án được chỉnh sửa.
    - Archived: Dự án được lưu trữ hoặc kết thúc.
- **Mô tả sự thay đổi trạng thái:**
    - Created → Updated: Khi thông tin dự án được chỉnh sửa bằng phương thức updateProjectData().
    - Updated → Archived: Khi dự án kết thúc hoặc không còn hoạt động.
- **Trạng thái của EmployeeAssignment:**
    - Assigned: Nhân viên được phân công vào dự án.
    - Reassigned: Nhân viên được phân công lại sang dự án khác.
    - Removed: Nhân viên bị loại khỏi dự án.
- **Mô tả sự thay đổi trạng thái:**
    - Assigned → Reassigned: Khi thay đổi nhiệm vụ hoặc dự án của nhân viên.
    - Assigned → Removed: Khi nhân viên không còn tham gia dự án.

### 2.4. PayrollProcessing
Mục tiêu: Tính toán lương và quản lý phiếu lương.
- **Trạng thái của Paycheck:**
    - Calculated: Phiếu lương được tính toán.
    - Verified: Phiếu lương được xác minh.
    - SentToBank: Phiếu lương được gửi đến ngân hàng.
    - Printed: Phiếu lương được in.
    - Completed: Quy trình xử lý lương hoàn tất.
- **Mô tả sự thay đổi trạng thái:**
    - Calculated → Verified: Khi phương thức PayrollCalculator.calculatePay() hoàn thành tính toán.
    - Verified → SentToBank: Khi phiếu lương được gửi đến BankSystem.
    - Verified → Printed: Khi phiếu lương được gửi đến PrintService để in.
    - SentToBank/Printed → Completed: Quy trình xử lý lương kết thúc.
- **Trạng thái của Timecard:**
    - Submitted: Thông tin giờ làm việc được nhập vào hệ thống.
    - Verified: Thông tin giờ làm việc được xác minh.
    - Approved: Thông tin giờ làm việc được chấp thuận cho tính lương.
- **Mô tả sự thay đổi trạng thái:**
    - Submitted → Verified: Khi dữ liệu giờ làm việc được kiểm tra.
    - Verified → Approved: Khi thông tin được chấp thuận và sẵn sàng để tính lương.

### Sơ Đồ
![](https://www.planttext.com/api/plantuml/png/b5KzRnD14EtzAqPfI91YYOyg1Kf888e4oCA61b6izpPtY-zsJtTh2mjHfOWG1OeeA11I34eJAIAHg7n5YelyF-uNy1UOsVlm-IDAgBmx-zxElRSpux_9vMPiM6JwWT-u0-t92AwEikGhc2WRZvGBnaj74hYdWQSZ3bwM768iIuxmZ6k5E8sh5Xj6slUXFOoD21fuqxqcF6QgbmTWdH3S4xpNm6n6m4gvNm4MGrXiu4C3uCtTjx2-_WYs8u581oF5oaPVCrywThS1UzCCJKU4EfPcTGtnKmmnsaAPZYOeKZfU-eTKIGNlIGz9kU38gQ5iSXs4liZJx4gcmScIpzmZEuwLXrxWBOkifqpwIoZP-CH05_sKI2am14UbfAvALSO-ae7tcz2Af39j4Gqa5pTQIDZMxNryAPWpx6YR0Z-udghf2YKYHE9rRL-6rjCPF5rWLrPiovFP-B8F_kHyGYM3tdeQRG93mfTnAv-UPSatIOHLKro2flq6NsAPzTUMkLMcdV7g0NcbtmbkdZF5N17Wi-mmmxeijiRbPtjgNqS1CrAhoiA5ayBCAdmBAr-5PK5kOpLzmlA8i-ICaPGBI4SAuIM4u5iHz-J0udSA1FHGkw7Y6bCjLeZ_4Va4gqWFXTYAO-agEYn5BfvOaM8XFACr3rknvR8id7Ax0I-yzAU2WKnF5Sw8_Z1B3XJ438l0gQJX0E6BbmHwi7135ni6V4sDWhGi-IBh7jOIJykXl6Z6gOVDSY2XOLmW2p_evX5a2KixYFcyxvSlNstoUIGYkI-jb4vwXczlDAcURO0Aj32FTh5I9EAIxnAKIrRGW77dETDcomaqZulnCiYI4-oWsu-mMfgvpwptLfrzOuDVCyAkUOUE30HdaLE-Gxctxs2ApSm3jFlTG9hS_sezR__ET7A0Ypy_m4-F0omjZ73euSz1W7zNRDxRhH3RVL3OD4-xEfgSPyal3g6Nde935Nv8YYjIJV2cK0xzZVu3003__mC0)

##  3 Xác định đúng các thuộc tính và mô tả rõ ràng
### 3.1. BankSystem
- **Lớp Paycheck:**
    - employeeID (String): Mã định danh của nhân viên nhận lương.
        - Mô tả: Xác định phiếu lương thuộc về nhân viên nào.
    - amount (Double): Số tiền trong phiếu lương.
        - Mô tả: Tổng số tiền mà nhân viên sẽ nhận.
    - date (Date): Ngày tạo phiếu lương.
        - Mô tả: Lưu ngày mà phiếu lương được tính toán hoặc gửi.
- **Lớp BankInformation:**
    - accountNumber (String): Số tài khoản ngân hàng của nhân viên.
        - Mô tả: Tài khoản mà lương sẽ được gửi vào.
    - bankName (String): Tên ngân hàng.
        - Mô tả: Ngân hàng nơi tài khoản được mở.
    - branchCode (String): Mã chi nhánh ngân hàng.
        - Mô tả: Xác định chi nhánh liên quan.
          
### 3.2. PrintService
- **Lớp Paycheck (kế thừa từ BankSystem):**
  - employeeID (String): Mã định danh của nhân viên.
            - Mô tả: Thông tin cần thiết để in phiếu lương.
    - amount (Double): Số tiền lương.
        - Mô tả: Hiển thị trên phiếu lương.
    - date (Date): Ngày lương được trả.
        - Mô tả: Hiển thị thông tin ngày in phiếu lương.
  - **Lớp EmployeeInformation:**
    - employeeID (String): Mã nhân viên.
        - Mô tả: Xác định nhân viên để in phiếu lương.
    - name (String): Tên nhân viên.
        - Mô tả: Hiển thị trên phiếu lương hoặc báo cáo.
    - department (String): Bộ phận mà nhân viên làm việc.
        - Mô tả: Phân loại nhân viên theo đơn vị công tác.
          
### 3.3. ProjectManagementDatabase
- **Lớp ProjectInformation:**
    - projectID (int): Mã định danh dự án.
        - Mô tả: Dự án mà nhân viên tham gia.
    - projectName (String): Tên dự án.
        - Mô tả: Nhận diện dự án trong cơ sở dữ liệu.
    - startDate (Date): Ngày bắt đầu dự án.
        - Mô tả: Theo dõi thời gian thực hiện dự án.
    - endDate (Date): Ngày kết thúc dự án.
        - Mô tả: Theo dõi thời hạn dự án.
- **Lớp EmployeeAssignment:**
    - employeeID (String): Mã nhân viên.
        - Mô tả: Gán nhân viên vào dự án.
    - projectID (int): Mã dự án.
        - Mô tả: Dự án mà nhân viên được phân công.
    - role (String): Vai trò của nhân viên trong dự án.
        - Mô tả: Xác định trách nhiệm cụ thể của nhân viên.
          
### 3.4. PayrollProcessing
- **Lớp Paycheck:**
    - employeeID (String): Mã định danh của nhân viên.
        - Mô tả: Phiếu lương được gán cho nhân viên này.
    - amount (Double): Tổng số tiền lương.
        - Mô tả: Số tiền sau khi tính toán từ giờ làm việc và các khoản phụ cấp.
    - date (Date): Ngày tính lương.
        - Mô tả: Ghi lại thời điểm lương được xử lý.
- **Lớp Timecard:**
    - hoursWorked (int): Số giờ làm việc của nhân viên.
        - Mô tả: Dữ liệu dùng để tính lương.
    - projectID (int): Mã dự án mà giờ làm việc thuộc về.
        - Mô tả: Phân loại giờ làm việc theo từng dự án.

### Sơ Đồ
![](https://www.planttext.com/api/plantuml/png/t5QzZjD04Exz5ACqG94NI7K_GIBISJem4lLclTZ6zgvbhoD5AFNLY9A68D4WeGE92XTN6EKz_0Iymirk76VjU1FgS-6VcTblvfjlTfD_vVrPBaacYoHsde2xMSFVZtNv2IvZakT00m4tP9c9E0PtcKkME1XrGNZKVAM4HiHdCDhRHl310RoeHi3LD60qQepg6WDBqbWi6PjD9-3ABEI-uII9ABYSm5GKyvWP3ez8XcQyjqO0dyddBThJPmTuEk9SGofl3rHx5QBsxP1NZa504PlnTo9BY0m5x_0Wb2hWwoAPiso0oXpNNfE43RaomcbmARn3vxPa4zh6wwB1j_hR9Bs8bRDIGjwWGReiMuIKxQKqhOzCp1RT8kXHBdnOIO-bk7yIfcWErNkQqJ49foswJKBndb7vad3KJeKXSJ8dUKTFIqXFt6sOhJLfuyREu7WSEYnphW-NwQ7Os6lk3TWrwLqfkcDcDjDxh6lkBcjd5FQIR5EVdfFpF0zzhdhs_sDYRHIUefRDVdf4ZdVaDI9RncDxUEDoof0BElTZqNSziht-9amO9PdN8H288ilVYYnYdcME-xhfJ2_souwDP5UUHe9N1U4GrEKj-65TtX6WrPf2N9UVKwTjydXyy4CpWP5Rbp_0gyjlt0SPLB_L8-J0_UehGbPVKBCEnD3nXZ0p3caGrd_k2uWtFpVh_hA1dTzBZeyxYB7ysqAz_u9gpOTJ6pi6CQx2wZk725DBM23Z40jHjLFDXUltXOePEQrSreAcHX4oOCAen3d3qqJzXNa0003__mC0)

## 4 Xác định đúng các phụ thuộc và quan hệ kết hợp
### 4.1. BankSystem
- **Phụ thuộc:**
    - **PayrollController → IBankSystem**
        - Loại: Dependency
        - Mô tả: PayrollController phụ thuộc vào IBankSystem để gửi yêu cầu giao dịch tiền lương.
        - Cách sử dụng: Gọi phương thức IBankSystem.deposit(aPaycheck, intoBank).
    - **IBankSystem → BankSystem**
        - Loại: Dependency
        - Mô tả: IBankSystem phụ thuộc vào BankSystem để thực hiện xử lý giao dịch thực tế.
- **Quan hệ kết hợp:**
    - **BankSystem → Paycheck**
        - Loại: Association
        - Mô tả: BankSystem liên kết với Paycheck để truy cập thông tin lương của nhân viên.
    - **BankSystem → BankInformation**
        - Loại: Association
        - Mô tả: BankSystem sử dụng thông tin từ BankInformation để thực hiện giao dịch.

### 4.2. PrintService
- **Phụ thuộc:**
    - **PayrollController → IPrintService**
        - Loại: Dependency
        - Mô tả: PayrollController phụ thuộc vào IPrintService để gửi yêu cầu in phiếu lương.
        - Cách sử dụng: Gọi phương thức IPrintService.printPaySlip(aPaycheck, employeeInfo).
    - **IPrintService → PrintService**
        - Loại: Dependency
        - Mô tả: IPrintService phụ thuộc vào PrintService để thực hiện lệnh in.
- **Quan hệ kết hợp:**
    - **PrintService → Paycheck**
        - Loại: Association
        - Mô tả: PrintService liên kết với Paycheck để sử dụng thông tin phiếu lương trong quá trình in.
    - **PrintService → EmployeeInformation**
        - Loại: Association
        - Mô tả: PrintService sử dụng thông tin nhân viên từ EmployeeInformation để tạo phiếu lương đúng.

### 4.3. ProjectManagementDatabase
- **Phụ thuộc:**
    - **PayrollController → IProjectManagementDatabase**
        - Loại: Dependency
        - Mô tả: PayrollController phụ thuộc vào IProjectManagementDatabase để truy xuất dữ liệu về dự án và nhân viên.
        - Cách sử dụng: Gọi phương thức fetchProjectData(projectID) hoặc fetchEmployeeAssignments(employeeID).
    - **IProjectManagementDatabase → ProjectManagementDatabase**
        - Loại: Dependency
        - Mô tả: IProjectManagementDatabase phụ thuộc vào ProjectManagementDatabase để xử lý dữ liệu thực tế.
- **Quan hệ kết hợp:**
    - **ProjectManagementDatabase → ProjectInformation**
        - Loại: Association
        - Mô tả: ProjectManagementDatabase liên kết với ProjectInformation để lưu trữ thông tin chi tiết về dự án.
    - **ProjectManagementDatabase → EmployeeAssignment**
        - Loại: Association
        - Mô tả: ProjectManagementDatabase sử dụng EmployeeAssignment để quản lý phân công nhân viên trong dự án.

### 4.4. PayrollProcessing
- **Phụ thuộc:**
    - **PayrollController → PayrollCalculator**
        - Loại: Dependency
        - Mô tả: PayrollController phụ thuộc vào PayrollCalculator để tính toán phiếu lương.
        - Cách sử dụng: Gọi phương thức PayrollCalculator.calculatePay(timecard).
    - **PayrollController → PrintService**
        - Loại: Dependency
        - Mô tả: PayrollController gửi yêu cầu in phiếu lương đến PrintService.
    - **PayrollController → BankSystem**
        - Loại: Dependency
        - Mô tả: PayrollController gửi yêu cầu chuyển tiền đến BankSystem.
- **Quan hệ kết hợp:**
    - **PayrollCalculator → Timecard**
        - Loại: Association
        - Mô tả: PayrollCalculator sử dụng thông tin từ Timecard để tính toán tiền lương.
    - **PayrollCalculator → Paycheck**
        - Loại: Association
        - Mô tả: PayrollCalculator tạo Paycheck sau khi tính toán lương.
## Sơ đồ 
![](https://www.planttext.com/api/plantuml/png/Z9HFQzim6CRl_XGlkJI5zGlqCCgwCGej19pBZfgYncfaoPDVXuNHmquxx5Hs7ZICCXYKjT1JVEZ18z_3ds1VOQyS1zkn7UQ3_-YLVdgUHvB_fiydCJABIQYy0_3NI_XpawVV8CoU0FFL3mZoz0iWtM_q54PiOOrIdXSnFcDJ0ODNJC_yHOmY7C0d3-ZYYiKnd5M5ihsu9Y8oiSGXWNWW-Em5k7vd-jBOaA4q-h3eUrqZTOCYQxY8ux5bEcRSZHpwQAMURW7NDP4ZAg0lx5noiIEpNchogPrK-af6DRLlmaYPXH1x5VSnfq8Bor2qiVkacol1yO9f-Wo5njSCsNiMjttqzAiBk1J8WxAdgmz9v-4nb2qrJnsM_WCVex6Yu7OwsUoTqMRXo6xJGLa-DHhTKzWwcJF54xM9pbNB2NPJBTBScYe_srRAYKgawPreE9QXuCnEsZJoTG2dsP93I0T3meU4wUAaU6qRHqSl6wVX60Ply_HUmYBxbG3FLpyJc4fcO9AdNtamw4CqTbKNH6g80fcldXDGwuVraXBkP_Kj9u77Dbd0noHVtQ7Jz1kK96U9Ut-4RAdxgErW2VQkqeVPlGu03I402VbPLpgzUa8ErWniJDa-SWYS4DrCgvbBeMCdgERWhfJsvB41xadhVFr0rgpBQPxTqbjdU5LcLJeElTrYZkJJWhenT_IZnI1xSW_ftERfTr3PRGXpn-83xqJeYVjX_mC00F__0m00)
