# LAB 5 Thiết kế các hệ thống con trong hệ thống Payroll System
## 1.Danh sách các hệ thống con:
- BankSystem
- PrintService
- ProjectManagementDatabase
- PayrollProcessing
  
## 2.Mô tả chi tiết từng hệ thống con:
### 2.1. BankSystem
- **Mục tiêu:** Xử lý việc gửi tiền lương trực tiếp vào tài khoản ngân hàng của nhân viên.
- **Các lớp thiết kế chính:**
  - IBankSystem: Giao diện xử lý giao dịch ngân hàng.
  - BankSystem: Hệ thống con xử lý giao dịch gửi tiền.
  - Paycheck: Phiếu lương được gửi.
  - BankInformation: Thông tin ngân hàng của nhân viên.
- **Mối quan hệ với các hệ thống khác:**
  - Tương tác với PayrollController để nhận yêu cầu gửi tiền.
- **Biểu Đồ BankSystem**
  
  ![](https://www.planttext.com/api/plantuml/png/j98n3i8m34NtdYBgL2IuG0U4OA4R4k80LceWQkgWs1qGucGC78ahq0GgsiAAXpYA_xD_eZnkzmKBU6bgcvn0Lt10bIw1gksP1UjKNHBLXhR0h3PmzixQbIC96Vsx6iCtzAvdatXwJM8o9EZte54LdxvziCIJOoCPjBW-egvorUscWNO1orLO2zexNuCOHuCPBtj_RjzHeuazwAN-VgNPR3wuVAxIWemO4EJENnhPlYfGGsWDLDenCY8wbq6_yKuZC_9FvSXy07PHUqqMI6Nu4Ky0003__mC0)

### 2.2. PrintService
- **Mục tiêu:** Xử lý việc in phiếu lương và cung cấp báo cáo lương.
- **Các lớp thiết kế chính:**
  - IPrintService: Giao diện xử lý yêu cầu in.
  - PrintService: Hệ thống con thực hiện in phiếu lương.
  - Paycheck: Phiếu lương cần in.
  - EmployeeInformation: Thông tin nhân viên dùng để in phiếu lương.
- **Mối quan hệ với các hệ thống khác:**
  - Tương tác với PayrollController để nhận yêu cầu in.
- **Biểu Đồ PrintService**
  
  ![](https://www.planttext.com/api/plantuml/png/l98x3i8m38RtdiBg119Se0D20ePkY9x0IjqIDKrAaY8Xr9CnS2IkG9C6gUMnuiMExS_-PULnkw-DHMtRMaGDiWfBWdYlkRGPwJDd5CCrWjwOG6DWZnUjXDWeQPqd7QhUT2j3VJRtsIxohXz6ka16a8udZz76vNiu4xoPOH-m8x4gWLUq0AeReIv4gInK0hlHIzTekPAJbK7jVxS5UfJw0Wx4vnsNozNRUHA83tHgoLWpA8uzEcros3kr9K4bMZ83yDaVXBfUN_pL-4M-OrB9H9kxyLsq9fcxl_C4003__mC0)

### 2.3. ProjectManagementDatabase
- **Mục tiêu**: Quản lý thông tin dự án, phân công nhân viên, và lưu trữ thông tin về công việc.
- **Các lớp thiết kế chính:**
  - IProjectManagementDatabase: Giao diện xử lý truy xuất dữ liệu dự án.
  - ProjectManagementDatabase: Hệ thống con lưu trữ và quản lý dữ liệu dự án.
  - ProjectInformation: Thông tin dự án.
  - EmployeeAssignment: Dữ liệu phân công nhân viên.
- **Mối quan hệ với các hệ thống khác:**
  - Cung cấp thông tin về dự án và phân công nhân viên cho PayrollProcessing.
- **Biểu Đồ ProjectManagementDatabase**
  
  ![](https://www.planttext.com/api/plantuml/png/p9AnJiGm38RtFaNKgJVS2zo03b663aWdti2aRWcaIR7TaofqJyR08_4A96s6GaLr8rwSsFc_s4w-FZwFB40oT3RhGRz2Yoe_aNz1BG_WmhP39oK8F05Zhjup5KnRO5Od6CbRU-UTH8-KifFHu5A-s4tHIpOvumIf0Osg-lEQ9QT1qS_fPCmN_RokoaDaxNwTlEzwwqV4MsRJkWZb0bFiXoILaphvRvLKhl7KWHZl5iarSfQk7sA_lzcQxq7bZ_Ws80khEWJp2RCXYBnDN8aMMn1a5R0qpi2hU8jMvxg439wHhq6i1n8HGNCsTIHSiYEwElxjRm000F__0m00)
  
### 2.4. PayrollProcessing
- **Mục tiêu**: Tính toán lương và quản lý thông tin thanh toán.
- **Các lớp thiết kế chính**:
  - PayrollController: Lớp điều khiển chính khởi chạy quy trình tính toán lương.
  - PayrollCalculator: Lớp xử lý tính toán lương.
  - Timecard: Chứa thông tin giờ làm việc của nhân viên.
  - Paycheck: Phiếu lương sau khi tính toán.
- **Mối quan hệ với các hệ thống khác**:
  - Tương tác với BankSystem để gửi tiền.
  - Tương tác với PrintService để in phiếu lương.
  - Nhận dữ liệu từ ProjectManagementDatabase về phân công nhân viên.
- **Biểu Đồ PayrollProcessing**
  
  ![](https://www.planttext.com/api/plantuml/png/V54z3i8W5Duv1M5gXrwWWsdYuDeOFG1vVQbDAIWF1cDwCWUFv1M4IZLDZM-1V7_l8pplZugSjCuFYfqbzB95BcfvjKQfsXf0eawtWjyO3mDA4l54RursyKIRs6cirudFyWaTsG-hLE2LT6PXXOHYK6Mk6n2aRKf-IBUyZ7Ou8VJhu5cqtFKMJzYwT55iVlGfkTZZnICv-XJgZ1QBaAyyXioxe_T8IF-qSwcetQ566vuR32EhK3Vn4ru0003__mC0)

## 3.Biểu đồ mô tả mối quan hệ giữa các hệ thống con

  ![](https://www.planttext.com/api/plantuml/png/b9DDJiCm48NtEONbVI_00XKeYowGgfOB3CuGJFmJF1Ea2FLaB3WILy1kAqWJ9nNUMDRtPkQDn_x-_5eIG-3Mcg81LKE5GcwW2zuOiUk8qKhnKOYuVl4jkFeSfQKC48dr7noGIH2hgHTKTKQ_Tiy-M63jtO7kYtCdcw0Txp2yQuKPBtqyB3g3ydxkRMDyXtZPatz5nG_Wuj6YunKmF07b3KveHsx_fHjQ73TnGwGhbpBbUpW-W9XEOLIwQkpz9BdpZjEEOOA3KQq1zaF-g2qg2ENSvPziZKg9nUAw_zB4bP0h7MBdeiJ6asOv5zYVVGezd6Fp7HdTN8YSc4DAiyMt5YacEef46PaiziKINPc-rmy0003__mC0)

- **Giải thích Các Mối Quan Hệ Giữa Các Hệ Thống Con**
### 3.1. PayrollController
- **Vai trò**: Là thành phần trung tâm của hệ thống, chịu trách nhiệm điều phối các tương tác giữa các hệ thống con.
- **Quan hệ**:
  - PayrollCalculator: Yêu cầu tính toán tiền lương dựa trên thông tin từ Timecard và dữ liệu dự án.
  - ProjectManagementDatabase: Truy xuất thông tin về phân công nhân viên và các dự án liên quan.
  - PrintService: Gửi yêu cầu in phiếu lương cho nhân viên.
  - BankSystem: Gửi yêu cầu gửi tiền lương trực tiếp vào tài khoản ngân hàng.
### 3.2. PayrollCalculator
- **Vai trò**:
  - Tính toán tiền lương của nhân viên dựa trên dữ liệu nhập (như Timecard và thông tin dự án từ ProjectManagementDatabase).
- **Quan hệ**:
  - Với ProjectManagementDatabase: Yêu cầu dữ liệu về nhiệm vụ hoặc thời gian làm việc của nhân viên.
  - Với BankSystem: Gửi thông tin tiền lương để thực hiện giao dịch ngân hàng.
  - Với PrintService: Cung cấp thông tin phiếu lương để in.
    
### 3.3. ProjectManagementDatabase
- **Vai trò**: Lưu trữ và cung cấp thông tin về dự án, nhân viên, và nhiệm vụ liên quan.
- **Quan hệ**:
  - PayrollController: Cung cấp dữ liệu về phân công nhân viên để hỗ trợ tính toán tiền lương.
  - PayrollCalculator: Cung cấp dữ liệu liên quan đến thời gian làm việc hoặc dự án.
    
### 3.4. BankSystem
- **Vai trò**: Xử lý giao dịch gửi tiền lương trực tiếp vào tài khoản ngân hàng của nhân viên.
- **Quan hệ**:
  - PayrollController: Thực hiện giao dịch khi nhận yêu cầu.
  - PayrollCalculator: Nhận thông tin phiếu lương để hoàn tất giao dịch.
    
### 3.5. PrintService
- **Vai trò**: Xử lý việc in phiếu lương của nhân viên.
- **Quan hệ**:
  - PayrollController: Thực hiện in khi nhận yêu cầu.
  - PayrollCalculator: Nhận dữ liệu phiếu lương để tạo bản in.
    
