# Lab2 - PHÂN TÍCH CA SỬ DỤNG VÀ VIẾT CODE JAVA CHO Maintain Timecard

## 1. Phân tích tất cả ca sử dụng còn lại
### 1.1 Phân tích ca sử dụng  Create Administrative Report
 #### 1.1.1. Xác định các lớp phân tích Create Administrative Report
  - Payroll Administrator: Người dùng tương tác với hệ thống, yêu cầu tạo và lưu báo cáo.
  - Report System: Chịu trách nhiệm xử lý yêu cầu từ Payroll Administrator để tạo báo cáo.
  - Report Criteria: Để thu thập các tiêu chí báo cáo do Payroll Administrator cung cấp.
  - Report: Đại diện cho báo cáo được tạo ra dựa trên tiêu chí đã nhập.
  - File System: Chịu trách nhiệm lưu báo cáo nếu Payroll Administrator yêu cầu lưu lại.
    
####  1.1.2. Thuộc tính và nhiệm vụ của từng lớp
  - Payroll Administrator
    - Thuộc tính: username, password
    - Nhiệm vụ: Yêu cầu tạo báo cáo, nhập tiêu chí báo cáo, yêu cầu lưu báo cáo và xác nhận lưu báo cáo.
      
  - Report System
    - Thuộc tính: Không có thuộc tính cần thiết cụ thể ở mức phân tích.
    - Nhiệm vụ: Xử lý yêu cầu tạo báo cáo, xác thực dữ liệu và kiểm tra tính hợp lệ của thông tin đầu vào.
      
  - Report Criteria
    - Thuộc tính: reportType (loại báo cáo), startDate (ngày bắt đầu), endDate (ngày kết thúc), employeeNames (tên nhân viên)
    - Nhiệm vụ: Lưu trữ các tiêu chí do Payroll Administrator nhập vào, cung cấp các tiêu chí cho hệ thống để tạo báo cáo.
      
  - Report
    - Thuộc tính: reportContent (nội dung báo cáo), createdDate (ngày tạo báo cáo)
    - Nhiệm vụ: Đại diện cho báo cáo được tạo dựa trên tiêu chí, lưu trữ nội dung và thông tin báo cáo.
      
  - File System
    - Thuộc tính: Không có thuộc tính cần thiết cụ thể ở mức phân tích.
    - Nhiệm vụ: Xử lý lưu báo cáo vào hệ thống file, kiểm tra vị trí lưu trữ và xác nhận tên tệp tin.

####  1.1.3. Biểu đồ Sequence cho ca sử dụng Create Administrative Report
  ![Diagram](https://www.planttext.com/api/plantuml/png/R98zRiCm38LtdOBer0Bf1J8KCTnwDcoWEskn1G5PSYacWC_MeKVg5Ih5SPmVU_2Wz_5Hxq5_Fx-xg2Ywxvt1JeD0ZQC4vmhRi-UeWlaG8zI56HB87G_e5HuQ6e8ej6DKwXyoqRIhH2ci98mJKwunatIjLEpeqhrgZQaBU7v9UxRGqFUUee86w8HG2UJeP9es8tMn89EGiEaQy7Wwq76W3TWq6pT0_U32I0GUUufFywPo2sy-ZTsQcAQSRr9BEB2bUwATYNTqdDSi6hgb5ZXasK3wJYFRf1qZdGhym4WMWb_cCxpQHSJ3kOd5SQMD71FGssd2XGwLWxymhkwZdMUkyEgSimp-awMVyUni3Rb8IrRsjsdptLuv3Wv7897qrbB_4R_8aBTcbtxvQVu3003__mC0)

####  1.1.4. Biểu đồ lớp (Class Diagram)
![Diagram](https://www.planttext.com/api/plantuml/png/d5D1JiCm4Bpd5NjifVG35geAHPmgX2WVi9AbikJOORqjYX0luy2J-09EOhkDItiWXqIQxEpixDW_Nzyhnv9ut-YYqj8vU98TMQrlwqOPvPWaMuAF0lopWBr3Ch910LicPNO1RZtntL8zWG48t_ReU4qe6P-njSIpUVZNaZse6jUa64d9X0VELXwEZCyYp3OYsyunDc4cWEgqVHNwYL0R-yyZ44W7gLNjQKd_2l7EMetIN1oGXayabg1j9LbP4xTnqY9p4aNIViTMBrsRRtW8wTuFBA1_1nHDVOurhROTugEFoGdO-0nlnbRBuC1X4fwT2vQvLZcLAQyfd6MLELjRmsWuCpScc5i1sA51waCQMPSpIlLHO3PF4ccW1wKnEphklo7-UKaMY-NqX8fuM893aAOUDCCsYadraPwEXUWld8Fe-rAzhni5NAWO_ftu5OEg0xRmwb5m0roiVB3znVy5003__mC0)
 ###### Mô tả quan hệ:
  - Payroll Administrator gửi yêu cầu đến Report System.
  - Report System phụ thuộc vào Report Criteria để lấy dữ liệu đầu vào.
  - Report System tạo ra Report dựa trên Report Criteria.
  - File System nhận Report để lưu vào hệ thống file nếu Payroll Administrator yêu cầu.
 
 #### 1.2.Phân tích ca sử dụng  Login
 ##### 1.2.1. Xác định các lớp phân tích
  - User: Người dùng thực hiện yêu cầu đăng nhập vào hệ thống.
  - LoginController: Lớp điều khiển quá trình đăng nhập, chịu trách nhiệm nhận thông tin đăng nhập từ người dùng và chuyển tiếp đến lớp AuthenticationService để xác thực.
  - AuthenticationService: Xác thực thông tin đăng nhập của người dùng bằng cách kiểm tra tên đăng nhập và mật khẩu.
  - UserAccount: Lưu trữ thông tin tài khoản của người dùng trong hệ thống, bao gồm tên đăng nhập và mật khẩu để kiểm tra xác thực.
    
 ##### 1.2.2. Thuộc tính và nhiệm vụ của từng lớp
  - User
    - Thuộc tính: username, password
    - Nhiệm vụ: Cung cấp thông tin đăng nhập để truy cập vào hệ thống.

  - LoginController
    - Thuộc tính: Không có thuộc tính đặc thù trong phân tích.
    - Nhiệm vụ: Điều khiển quá trình đăng nhập, tiếp nhận thông tin đăng nhập từ người dùng và gọi lớp AuthenticationService để kiểm tra xác thực.

  - AuthenticationService
    - Thuộc tính: Không có thuộc tính đặc thù trong phân tích.
    - Nhiệm vụ: Kiểm tra xác thực thông tin đăng nhập bằng cách so sánh thông tin nhập vào với dữ liệu trong UserAccount. Trả về kết quả xác thực cho LoginController.

  - UserAccoun
    - Thuộc tính: username, hashedPassword
    - Nhiệm vụ: Lưu trữ thông tin tài khoản của người dùng, cung cấp thông tin cho lớp AuthenticationService để kiểm tra xác thực.
      
 ##### 1.2.3. Biểu đồ Sequence cho ca sử dụng Login
![Diagram](https://www.planttext.com/api/plantuml/png/P94nRiCm34LtdOB8b00jkdie8dZrPlW0XCou0cJ9eAZaS1rwf5wXbEEu3Qf103-VFadn-_Fhd0LPoXmCEaaCGoOsYqhU-GMZmA5BauzjYi8f1E83O8QkVMPiaG-A6gFu57lYgtUqahP_9gk_TIwLA6j-iCPK3LxVrRK1TT6Wg19n9i0ume8vtnAFfcihPVi6yBSU7H_moqwUZEqhEjW69f8_DNVuP0RxS6EImX7mZe2FbxGPr8wk6FoupgLWBa7Wc8jpbFFR1Nqeh5wewYOQq7FljDPj8DJ_sxCKCi7sxXzApBg2MJcSo50SpLclkfmV0000__y30000)

  ##### 1.2.4. Biểu đồ lớp (Class Diagram)
![Diagram](https://www.planttext.com/api/plantuml/png/Z58xJWCn4ErzYYc3n5vW2vIG2ea2AU808tkoQycP0NkS514de-18N04xh99DTYLmv-Tv7p_x-_DhcHIZvbqmDc1Ay9eemj50MGtaic7SKGiRZPwx0NuhWmU9xWe62D9vNjoP3pDeFLTWBQnHGZZB0c3MdbYzHQNgjxZrkPzOZ5HN5xONtb3SUqjdxJq6xuhkEfAhKnZIV-HRU1G9X7pngSbMrafc_QkG7bDFxcM-bevqa7dYhKp25EkHKxK_FK7JF4pwQtyhXaZlcPAQs_FAcM-dlUhSp0zL-lZIXMGjbIPm07p9RvR4hdwN7m000F__0m00)
 ###### Mô tả quan hệ:
  - User tương tác với LoginController để cung cấp thông tin đăng nhập.
  - LoginController đóng vai trò kiểm soát, gửi yêu cầu xác thực đến AuthenticationService.
  - AuthenticationService xác thực bằng cách kiểm tra thông tin với UserAccount và trả về kết quả xác thực cho LoginController.

 #### 1.3. Phân tích ca sử dụng  Maintain Employee Information
 ##### 1.3.1. Xác định các lớp phân tích
  - PayrollAdministrator: Người thực hiện thao tác thêm, cập nhật hoặc xóa thông tin nhân viên.
  - EmployeeController: Lớp điều khiển quy trình quản lý thông tin nhân viên, bao gồm việc tiếp nhận yêu cầu từ Payroll Administrator và chuyển thông tin đến các lớp dịch vụ để thực hiện các thao tác thêm, cập nhật hoặc xóa.
  - EmployeeService: Lớp xử lý chính để thêm, cập nhật và xóa nhân viên, chịu trách nhiệm xác thực các yêu cầu và giao tiếp với cơ sở dữ liệu để thực hiện các thao tác quản lý nhân viên.
  - Employee: Đại diện cho thông tin của từng nhân viên, bao gồm các thuộc tính như mã nhân viên, loại nhân viên, địa chỉ, số an sinh xã hội, mức lương, và các khoản khấu trừ.
  - Database: Lớp lưu trữ thông tin nhân viên và chịu trách nhiệm quản lý dữ liệu nhân viên một cách an toàn và chính xác.

 ##### 1.3.2. Thuộc tính và nhiệm vụ của từng lớp
  - PayrollAdministrator
    - Thuộc tính: adminID, name
    - Nhiệm vụ: Yêu cầu thêm, cập nhật hoặc xóa thông tin nhân viên trong hệ thống.

  - EmployeeController
    - Thuộc tính: Không có thuộc tính đặc thù trong phân tích.
    - Nhiệm vụ: Điều khiển quy trình quản lý thông tin nhân viên, nhận yêu cầu từ Payroll Administrator và điều phối đến EmployeeService để thực hiện.

  - EmployeeService
    - Thuộc tính: Không có thuộc tính đặc thù trong phân tích.
    - Nhiệm vụ: Thực hiện các thao tác thêm, cập nhật và xóa nhân viên trong hệ thống bằng cách gọi đến Database để lưu trữ và truy xuất thông tin.

  - Employee
    - Thuộc tính: employeeID, name, type, address, SSN, deductions, phone, hourlyRate, salary, commissionRate, hourLimit
    - Nhiệm vụ: Lưu trữ thông tin chi tiết của nhân viên.

  - Database
    - Thuộc tính: employees: List<Employee>
    - Nhiệm vụ: Lưu trữ tất cả các thông tin nhân viên, hỗ trợ thêm, cập nhật và xóa dữ liệu nhân viên theo yêu cầu.

 ##### 1.3.3. Biểu đồ Sequence cho ca sử dụng "Maintain Employee Information"
 ![Diagram](https://www.planttext.com/api/plantuml/png/R95DQiCm48NtEiMGLG993-15IMrhqLt19vZ8Kr2nVZeQf_XiNVH8lKBbtnBmHeWtttkZXtw_Vwv9aALtdK8ZWU4D1mvTzz8wwsqInYogc15hR4GlSD0kTc4WgeAN4IK-02RGrJxM4D-jePbf7faQ1M-Ovc5TAl9YPVZtpYONbTfx5boUyzO2c3vxIW8I0DiMQ34hNKr4Kupo6ddqwEWCCiHyPfqffJEGcAUJqiraSB40muH2uEaBz9Rd8boMH2RfsM-x8Dm-oCYIK9S59BpJDZwkbvEgoot31FzksQ7Ou2VdqcU5N-kfGbRtsZzmL_Bj-8T_0000__y30000)
 
 ##### 1.3.4. Biểu đồ lớp (Class Diagram)
![Diagram](https://www.planttext.com/api/plantuml/png/Z5DBJiCm4Dtx55uMYLmWGbKHPL6fgX0vmM1FMql-HFO4AKASZ0L7uWeuD0v9d2AoovltdiTlnbyVdvj0uAancWaD8V0dQBtJ-buQPLKW3-GyVsCyVWM73jrjIrwHL_RKenOCJY3E3LWuuQEfjMiHLpVidVN-2Njmbhg3CBdpw2v7YWlMr188CrYYHlhJlqB_gWGEviBZnAWSc8idxUpHhJ3z33VEPRDE5YHvRqEUEVjQf0Mdjfv3CJ2F8SpGgZhC48co4QISZTHz7EhTfRhko_NPsRdrsJLUjyynaP8VjGFgyG0QV3l5X3D6XH3zStxdirT6KScLfJwp4z8avr54Mo1uWP17b5fFmlN2qYJkxv2kh56U-os_BlxVY1SVJb6ibpQ-x1y8MwYD9Mc9ovZn3u7DAsDsf84GSI4MMKEo9G-nDMGRjB9xzzy0003__mC0)
  ###### Mô tả quan hệ:
  - PayrollAdministrator tương tác với EmployeeController để thêm, cập nhật hoặc xóa nhân viên.
  - EmployeeController điều khiển luồng xử lý, chuyển yêu cầu đến EmployeeService.
  - EmployeeService xử lý thao tác, gọi đến Database để lưu trữ hoặc lấy thông tin nhân viên.
  - Database lưu trữ tất cả dữ liệu nhân viên, cung cấp các thao tác để quản lý thông tin nhân viên.

 #### 1.4. Phân tích ca sử dụng  Maintain Purchase Order
 ##### 1.4.1. Xác định các lớp phân tích
- Commissioned Employee: Người dùng có quyền truy cập vào hệ thống để thực hiện các thao tác tạo, cập nhật, và xóa đơn hàng.
- Order System: Xử lý các yêu cầu từ nhân viên và điều hướng các thao tác cần thực hiện đối với đơn hàng.
- Purchase Order: Đại diện cho một đơn hàng cụ thể, lưu trữ thông tin chi tiết của đơn hàng.
- Customer: Lưu trữ thông tin về khách hàng liên quan đến đơn hàng.
- Product: Lưu trữ thông tin về sản phẩm trong đơn hàng.

 ##### 1.4.2. Thuộc tính và nhiệm vụ của từng lớp
- Commissioned Employee
  - Thuộc tính: employeeId, name, username, password
  - Nhiệm vụ: Yêu cầu thực hiện các thao tác thêm, sửa, hoặc xóa đơn hàng.
    
- Order System
  - Thuộc tính: Không có thuộc tính đặc thù trong phân tích.
  - Nhiệm vụ: Nhận yêu cầu từ Commissioned Employee, xác thực quyền truy cập và điều hướng đến các chức năng thêm, sửa, hoặc xóa đơn hàng.
    
- Purchase Order
  - Thuộc tính: orderId, customer, billingAddress, productList, date, status
  - Nhiệm vụ: Lưu trữ và quản lý thông tin chi tiết của đơn hàng. Cung cấp chức năng cập nhật thông tin đơn hàng khi cần thiết.
    
- Customer
  - Thuộc tính: contactName, billingAddress
  - Nhiệm vụ: Lưu trữ thông tin liên hệ và địa chỉ thanh toán của khách hàng
    
- Product
  - Thuộc tính: productId, productName, quantity, price
  - Nhiệm vụ: Lưu trữ thông tin chi tiết của sản phẩm trong đơn hàng.
    
 ##### 1.4.3. Biểu đồ Sequence cho ca sử dụng Maintain Purchase Order
![Diagram](https://www.planttext.com/api/plantuml/png/p5GxRiCm3Drr2g9J0hZ8dg588NleP2D63w1QT2f07rUIK-Hi7NgaNg6IFqdaPEXO3uO1FRuFIVddwtldFBE-LvAmnXiBr2Wbd1D68ozK9yq94PW3Mf0k04KZEgOzF9IMeuNwv3ogXmWewnHGzRPvPmvXG0wGgamXj7VUgEcGBigjuNtZnpf2Q06FJq5Z2tlywD5vy0OOvvk-uypZXgD4Zz3DeYQAahAELRIuLBMzRdm81ojgCHHcy3eGP90F3EihfRh3HhIdSmqXJ7eOwo2DHo0yjsgf7U3ecP0ELiqKF8Ct8QNGXnZ5edCPT6Fky1LjhGVYYwNGbQFWovmpyPMBgjpEJZL-tdDRbJFfSnZtGKElHN0zCRxaYqYpScGxGr06oh61Vsj8GduRwuvs3B97RmKUmnvg3aUqSIYBIQTokN2TP4jGqgPRyN6JE0ZT6glOCF7KnvGq9KFDnyKO5-XVzO4QtGghOBWTSvwBt7IyKCdlNgKOSnTUyK_n2m00__y30000)

  ##### 1.4.4. Biểu đồ lớp (Class Diagram)
  ![Diagram](https://www.planttext.com/api/plantuml/png/V5J1JkCm4BtdA-ROIbJSBHQnQlU0jCiY41zWx2bhoR63PonK8RwC0v_4BwmJEsaT8dg8gZTlCk-zcVRp_UEAM0QEhMsKbKImzMrhY8ntg7-rdVK7H7Xj87qsW0MurWBkEHZtL0fEjZY38c5OWBiqvCM7-WK00PyZ4l_K-c_G65Rh6d_ej6HSBEtGuh7qrXGV0t1_8CQso0VeWbT8D9JkSlUA3zqayGnyNpgwWn_WehNZH1LmKg6HfR4au8_irW9kOr3_9ELYeSSJqRCNdq7LNnhqYPLPmucpQjIqcXc_e2eI-nQ3W6tvLWgFnjf4Itc7bCXyHy7hgFYt8HRGFozkCt9P2Bql0RlqB40w8euqs-aJfkKCBbVhmMULorYgWvXSZdedWyexbefllfxKDru64TlSUUtsVXHo33CRcwOKwr-2BFZ2zESe7Hi-232E9xPHYQTzVBHu55A6pK99MXP_T9lDPNN5Ohnuoik6v2brK7DAwflg0n7bREayvqxd-SoegNbzvnHwFskF0PrQv8sfYRmLaqHSeTFzlyX_0000__y30000)
 ###### Mô tả quan hệ:
- Commissioned Employee liên kết với Order System để yêu cầu các thao tác với đơn hàng.
- Order System liên kết với Purchase Order để xử lý các yêu cầu tạo, cập nhật hoặc xóa đơn hàng.
- Purchase Order liên kết với Customer để lưu thông tin về khách hàng của đơn hàng.
- Purchase Order cũng liên kết với Product để lưu thông tin sản phẩm được mua.
  
 #### 1.5. Phân tích ca sử dụng  Run Payroll
 ##### 1.5.1. Xác định các lớp phân tích
- PayrollSystem: Điều khiển quy trình chạy bảng lương và xử lý các yêu cầu liên quan đến tính toán và gửi thanh toán cho nhân viên.
- EmployeeService: Lớp cung cấp dữ liệu về nhân viên, bao gồm thông tin như lương, loại nhân viên, các khoản khấu trừ và các hình thức nhận lương.
- Employee: Đại diện cho mỗi nhân viên trong hệ thống với các thuộc tính như ID, loại nhân viên, hình thức thanh toán, và các thông tin cá nhân liên quan đến tính lương.
- Timecard: Lưu trữ thông tin về giờ làm việc của nhân viên để phục vụ tính toán lương cho nhân viên hưởng lương theo giờ.
- BankSystem: Xử lý các giao dịch ngân hàng đối với nhân viên chọn phương thức thanh toán qua tài khoản ngân hàng.
- Database: Lưu trữ dữ liệu nhân viên và bảng lương để hỗ trợ quy trình xử lý thanh toán.

 ##### 1.5.2. Thuộc tính và nhiệm vụ của từng lớp
- PayrollSystem
  - Thuộc tính: currentDate
  - Nhiệm vụ: Tự động kích hoạt quy trình chạy bảng lương theo lịch định kỳ (thứ Sáu và ngày cuối tháng), truy xuất danh sách nhân viên cần thanh toán, tính toán lương và xử lý việc thanh toán qua hệ thống ngân hàng hoặc in phiếu lương.

- EmployeeService
  - Thuộc tính: Không có thuộc tính đặc thù trong phân tích.
  - Nhiệm vụ: Cung cấp thông tin chi tiết của nhân viên (thời gian làm việc, lương, phương thức nhận lương, và các khoản khấu trừ).
- Employee
  - Thuộc tính: employeeID, name, type, salary, payMethod, benefits, deductions
  - Nhiệm vụ: Lưu trữ thông tin về nhân viên, bao gồm các yếu tố lương, loại hình trả lương, và phương thức nhận lương.

- Timecard
  - Thuộc tính: hoursWorked, date
  - Nhiệm vụ: Lưu giữ dữ liệu về số giờ làm việc của nhân viên theo từng ngày.

- BankSystem
  - Thuộc tính: Không có thuộc tính đặc thù trong phân tích.
  - Nhiệm vụ: Nhận và xử lý các giao dịch ngân hàng đối với các khoản thanh toán qua tài khoản ngân hàng.

- Database
  - Thuộc tính: employees, timecards
  - Nhiệm vụ: Lưu trữ thông tin nhân viên và bảng chấm công phục vụ cho quy trình tính toán và lưu trữ bảng lương.

 ##### 1.5.3. Biểu đồ Sequence cho ca sử dụng Run Payroll
![Diagram](https://www.planttext.com/api/plantuml/png/R5DBJiCm4Dtx5BDC9Ng1Bb2Lfgn0YfHSm3XJiEB4mPvKojbOS2IkmDZDfmQoyU9zPqRv_lmwUfAEniw8WL-jz21xWb9EpXfJJPwm0-cXh1Byt0t6JeWLkgjM61Zd_naHweO4gtM7IhecOFKfWNBPjrjgddeMakIhzD6po8KeAzW_Sl01tf2MG5zRRf-fqJdiYIMu4-T8BF83V8pe9i252y6k0Tl37LyKEUnduvNvh3r57mRAFy1SfJx5Aijy_icwjLQMA7QYFYsT79BJU4MWHGSNwxQ4fKzmNoanDdZCVL9WMKqt7419eqR3Syr7pHBg0_pgnPhLTBWf2YIfZHT26Zw2TgZumS5wJGBukuNbB50EEIWSiNQozrAHjdsMskoY9jzMIHkr8acZ5sZuo2zC1jv3gLMx7uUxf5ZDwPvu8lMEglsJW7rpsy7CRj0WuJegw0jqqhLy-h3fY7AwEB8k_0e_0000__y30000)

 ##### 1.5.4. Biểu đồ lớp (Class Diagram)
![Diagram](https://www.planttext.com/api/plantuml/png/X5D1QiCm4Bpx5JewXtn051DAUYYqK4YWvusyIKnaoTMk0gRqPJtqIVr2vKHo73jjVGZMpEvcTaR-_lnQ48DZN-jCQI0IBz0wg_Mg9SPQl6SYF7EXl7DeU0cCKdI_9rm8vqrio6SHQbnbE81gZ-gGDsTsYGoL9fd6ntFgKGx3p7imXxK3Gw2uiYOlVslwoABOXxhHjaLSeJjM2gDS8NR8YQAr3UrvsIkVIV5K4T-bWc8whbyR8_2ub6B5OR5T90pKE8AuRSOGWGRNIh7L5ZXYmP1dvBqjHxKRDBYjcAAwCrT4iiJIdpovHGVxG2klmsuf2wvgLE3ALBwEvsBWNSBwPVVMEtgrxe11MyWm_VSbyxwtI-hgXdInMuL4m_puylv7Xc4oR82cfjCag6ZqRyj59MyUNTl7_r_or_TzFYycbqeAKDrgsPZeYdlrKZWCeU0HRupilPR2qws2WQ5I49fou6Es2EVk0_q1003__mC0)
 ###### Mô tả quan hệ:
  - PayrollSystem tự động khởi chạy quy trình tính toán lương và xử lý thanh toán, với các tương tác để lấy thông tin nhân viên, tính toán và xử lý thanh toán.
  - EmployeeService cung cấp dữ liệu nhân viên, và Timecard cung cấp dữ liệu giờ làm để tính toán cho nhân viên hưởng lương theo giờ.
  - BankSystem chịu trách nhiệm xử lý các giao dịch đối với các nhân viên nhận lương qua tài khoản ngân hàng.
  - Database lưu trữ thông tin nhân viên và bảng chấm công để phục vụ cho quy trình tính toán lương.
    
 #### 1.6. Phân tích ca sử dụng  Create Employee Report
 ##### 1.6.1. Xác định các lớp phân tích
- ReportSystem: Điều khiển quy trình tạo báo cáo cho nhân viên theo các tiêu chí và thông tin nhập vào.
- EmployeeService: Lớp cung cấp dữ liệu nhân viên cần thiết cho các báo cáo, bao gồm giờ làm việc, dữ liệu nghỉ phép/ốm, và tổng lương theo năm.
- ProjectManagementDatabase: Cung cấp danh sách các số liệu liên quan đến dự án khi cần lấy thông tin làm báo cáo cho các dự án cụ thể.
- Report: Đại diện cho một báo cáo với các thuộc tính như loại báo cáo, ngày bắt đầu, ngày kết thúc, và kết quả báo cáo.
- Employee: Đại diện cho người dùng là nhân viên, có thể tương tác với hệ thống để tạo và lưu báo cáo.
- FileSystem: Xử lý việc lưu và quản lý các tệp báo cáo nếu nhân viên yêu cầu lưu báo cáo.
 ##### 1.6.2. Thuộc tính và nhiệm vụ của từng lớp
- ReportSystem
  - Thuộc tính: reportType, startDate, endDate
  - Nhiệm vụ: Điều khiển quy trình tạo báo cáo, bao gồm lấy thông tin từ EmployeeService và ProjectManagementDatabase dựa trên tiêu chí báo cáo, hiển thị báo cáo cho nhân viên và hỗ trợ tùy chọn lưu báo cáo.

- EmployeeService
  - Thuộc tính: Không có thuộc tính đặc thù trong phân tích.
  - Nhiệm vụ: Cung cấp dữ liệu về giờ làm việc, nghỉ phép/ốm, và tổng lương cho báo cáo nhân viên.

- ProjectManagementDatabase
  - Thuộc tính: chargeNumbers
  - Nhiệm vụ: Cung cấp danh sách các số liệu (mã dự án) để nhân viên lựa chọn khi tạo báo cáo cho một dự án cụ thể.

- Report
  - Thuộc tính: type, startDate, endDate, data, chargeNumber (nếu có)
  - Nhiệm vụ: Lưu giữ thông tin của báo cáo, bao gồm loại báo cáo và kết quả từ EmployeeService hoặc ProjectManagementDatabase.

- Employee
  - Thuộc tính: employeeID, name
  - Nhiệm vụ: Là đối tượng người dùng có thể tương tác với hệ thống để tạo và lưu báo cáo.

- FileSystem
  - Thuộc tính: filePath, fileName
  - Nhiệm vụ: Quản lý các thao tác lưu báo cáo vào hệ thống nếu nhân viên chọn lưu báo cáo.

 ##### 1.6.3. Biểu đồ Sequence cho ca sử dụng "Create Employee Report"
![Diagram](https://www.planttext.com/api/plantuml/png/Z5F1Ri8m3BtdAt84QVm0Xmc93kqm4298EvlMGBQqwPmKgT-smpvflp0dBIMTaBOUMaj-Vdv-Thy_lnRE0_ccDABchyvr3PMNJsLjR8iemOLubDjXRSchrdaiGtwdxfOgf8lEEuOnOals3NE_XWfEM6BbC_1m01UnstLsfrliWsCTAstmfcAbXE3MSlR8WkQIyAD1vxlgoLJiLCWmO4WjINia3HEAc7rRuuECPh0S3h4gGZ1DMMko5rtWlqi562_treEHpxOX9ryjlMCXZvOaN7qGafzE7my_boVqopFG2JTDUK1oh3uWE2TdlOuypRzebtACPanm2WqtqxRg-PAnN4obOCRm4E9gcuggEZF3ilxsJ0rQQQZgsPWcq5L83EqNbF8L39sAT6E5ThM1TbXcAXqkFKU6kNRTUC5rnOd-U19pLgEIoP5FQ0CbDmtH5lovysPrav_RwgYfXE2SGCD7cccN0nM_oM_MnuCjEXGMqSW5ly8_zWC00F__0m00)
 
 ##### 1.6.4. Biểu đồ lớp (Class Diagram)
 ![Diagram](https://www.planttext.com/api/plantuml/png/d5D1JiCm4Bpd5JucKlC12rML24X8K5M43spT9JMAdM0xbIB4opZm9Bw0anWdiTKBEVWmkpipzcn-lhvtse0odQWJLeFMv1dRHfcormO5-KY8_NAYHl2bRv6IqYWkArSOXmim5XzEXw8y1HYn5EyTQZFHfvb3AvIeR5C0QxZCq6VYhDs9jcvwn1BLXJDqxWOIHslb88szRaARcxN3Z99vVfOxgEODcNa22HKAb6Fv21hzix0pg0htdJYYqfGyScrk9idjRErssPHcGPjNcnnuQlF_jyx9oHeDXfTMVIbwMI-F3dWe0Xu9OkthMh9pX0KohdaZbr7Uyng37Nkrq07CEH0Su7qi6cx8QctpV1ij2oN066eTTrxFcVxTBHvoSL6_mN7Buevqz9liR5Z3d_OB003__mC0)
  ###### Mô tả quan hệ:
- ReportSystem điều khiển quy trình tạo và lưu báo cáo, với các thao tác như lấy dữ liệu, tạo báo cáo, hiển thị và xử lý yêu cầu lưu.
- EmployeeService cung cấp dữ liệu về giờ làm việc, nghỉ phép/ốm, hoặc tổng lương cho báo cáo nhân viên.
- ProjectManagementDatabase cung cấp danh sách mã dự án để sử dụng khi cần thiết.
- Report lưu giữ dữ liệu của báo cáo bao gồm loại báo cáo, khoảng thời gian và thông tin dự án nếu có.
- FileSystem hỗ trợ lưu báo cáo khi Employee chọn thao tác lưu.

## 2. Code Java mô phỏng ca sử dụng Maintain Timecard.
  ```java
                               import java.time.LocalDate;
                                import java.util.HashMap;
                                import java.util.Map;
                                import java.util.Scanner;
                                
                                class Timecard {
                                    private final LocalDate startDate;
                                    private final LocalDate endDate;
                                    private LocalDate submittedDate;
                                    private boolean isSubmitted;
                                    private Map<String, Integer> hoursWorked;
                                
                                    public Timecard(LocalDate startDate, LocalDate endDate) {
                                        this.startDate = startDate;
                                        this.endDate = endDate;
                                        this.isSubmitted = false;
                                        this.hoursWorked = new HashMap<>();
                                    }
                                
                                    public boolean isSubmitted() {
                                        return isSubmitted;
                                    }
                                
                                    public void addHours(String chargeNumber, int hours) {
                                        hoursWorked.put(chargeNumber, hoursWorked.getOrDefault(chargeNumber, 0) + hours);
                                    }
                                
                                    public boolean validateHours(int hours) {
                                        return hours >= 0 && hours <= 24;
                                    }
                                
                                    public void submit() {
                                        if (!isSubmitted) {
                                            this.submittedDate = LocalDate.now();
                                            this.isSubmitted = true;
                                            System.out.println("Timecard submitted on: " + submittedDate);
                                        } else {
                                            System.out.println("Timecard has already been submitted and cannot be changed.");
                                        }
                                    }
                                
                                    public void display() {
                                        System.out.println("Timecard Period: " + startDate + " to " + endDate);
                                        System.out.println("Hours Worked by Charge Number:");
                                        hoursWorked.forEach((chargeNumber, hours) -> 
                                            System.out.println("  " + chargeNumber + ": " + hours + " hours"));
                                    }
                                }
                                
                                public class TimecardSystem {
                                    private Timecard currentTimecard;
                                    private final Scanner scanner;
                                
                                    public TimecardSystem() {
                                        this.scanner = new Scanner(System.in);
                                    }
                                
                                    public void start() {
                                        System.out.println("Welcome to the Timecard System.");
                                        if (currentTimecard == null || currentTimecard.isSubmitted()) {
                                            LocalDate start = LocalDate.now().withDayOfMonth(1);
                                            LocalDate end = start.plusWeeks(1).minusDays(1);
                                            currentTimecard = new Timecard(start, end);
                                        }
                                        mainMenu();
                                    }
                                
                                    private void mainMenu() {
                                        while (true) {
                                            System.out.println("\nMain Menu:");
                                            System.out.println("1. View Timecard");
                                            System.out.println("2. Add Hours");
                                            System.out.println("3. Submit Timecard");
                                            System.out.println("4. Exit");
                                            int choice = scanner.nextInt();
                                            scanner.nextLine(); // Consume newline
                                            switch (choice) {
                                                case 1 -> viewTimecard();
                                                case 2 -> addHours();
                                                case 3 -> submitTimecard();
                                                case 4 -> exitSystem();
                                                default -> System.out.println("Invalid choice. Please try again.");
                                            }
                                        }
                                    }
                                
                                    private void viewTimecard() {
                                        if (currentTimecard != null) {
                                            currentTimecard.display();
                                        } else {
                                            System.out.println("No timecard available.");
                                        }
                                    }
                                
                                    private void addHours() {
                                        if (currentTimecard.isSubmitted()) {
                                            System.out.println("Timecard is already submitted. No changes allowed.");
                                            return;
                                        }
                                        System.out.print("Enter charge number: ");
                                        String chargeNumber = scanner.nextLine();
                                        System.out.print("Enter hours worked (0-24): ");
                                        int hours = scanner.nextInt();
                                        scanner.nextLine(); // Consume newline
                                        if (currentTimecard.validateHours(hours)) {
                                            currentTimecard.addHours(chargeNumber, hours);
                                            System.out.println("Hours added successfully.");
                                        } else {
                                            System.out.println("Invalid hours entered. Please enter a value between 0 and 24.");
                                        }
                                    }
                                
                                    private void submitTimecard() {
                                        if (currentTimecard.isSubmitted()) {
                                            System.out.println("Timecard has already been submitted.");
                                            return;
                                        }
                                        System.out.println("Submitting timecard...");
                                        currentTimecard.submit();
                                    }
                                
                                    private void exitSystem() {
                                        System.out.println("Exiting the Timecard System. Goodbye!");
                                        System.exit(0);
                                    }
                                
                                    public static void main(String[] args) {
                                        TimecardSystem system = new TimecardSystem();
                                        system.start();
                                    }
                                }
