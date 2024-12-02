# Lab 4. Thiết kế các ca sử dụng cho hệ thống "Payroll System" và viết tài liệu giải thích lý do đưa ra thiết kế đó

## 1. Thiết kế các ca sử dụng cho hệ thống "Payroll System"
  ### 1.1. Danh sách các ca sử dụng
#### 1.1.1. Ca sử dụng chính
  - 1.1.1.1 **Deposit Paycheck (Gửi tiền lương)**
    - **Mô tả**: Gửi tiền lương của nhân viên vào tài khoản ngân hàng qua hệ thống.
    - **Tác nhân chính**: Payroll Manager.
    - **Tác nhân phụ**: BankSystem.
    - **Luồng sự kiện chính**:
      - Payroll Manager chọn nhân viên cần trả lương.
      - Hệ thống truy vấn tài khoản ngân hàng của nhân viên.
      - Hệ thống gửi yêu cầu giao dịch tới BankSystem.
      - Ngân hàng xác nhận giao dịch thành công.
      - Hệ thống cập nhật trạng thái giao dịch.
    - **Kết quả**: Tiền lương được gửi tới tài khoản ngân hàng của nhân viên.
  - **Sở Đồ**:

  ![](https://www.planttext.com/api/plantuml/png/L911IiD058RtSugVhXJq0br8YGiL30IoSJjEuyoGz4rCfaBMBbo8TqWL4OI22rUPHHU1tcDEu1KwKLlQxNlVzx-Vz-DMazhooivd1UF2cWe9RofJ534dBhCAl4OIip8WMkYIayNedq3Qr3QRZNwHz129EELxwoXbB8bnUXR0CSwLToy4KlqhuK7tdmJXkm-2z6wfKQo_rWkIB4ctmhNltXjOrN-JXDK4sxSQkJA-UmivSiXHVRjpek1S_6LvzqGAKdE3gNVFGk6ev8rGcSXFS1jQNj6TEMRHxjPDln2Xck-MTA0f4muC7LfIsshn69VQkyTX7YZalbjPtCz3hNsNJJAQ3W_U0000__y30000)

  - 1.1.1.2 **Print Paycheck (In phiếu lương)**
    - **Mô tả**: In phiếu lương cho nhân viên.
    - **Tác nhân chính**: Payroll Manager.
    - **Tác nhân phụ**: PrintService.
    - **Luồng sự kiện chính**:
    - Payroll Manager yêu cầu in phiếu lương cho nhân viên.
      - Hệ thống truy vấn thông tin phiếu lương từ cơ sở dữ liệu.
      - Hệ thống gửi lệnh in tới PrintService.
      - Phiếu lương được in và trả về Payroll Manager.
  - **Sở Đồ**:

  ![](https://www.planttext.com/api/plantuml/png/V90nIWGn58RxdEAnbO9UO0lPGX2BWO6nq3B6C0bctuGtoS2SmDeRE8W8meA5rKonHMJlaHDu1HFTQRROxXNV_ty_xsVQhbh7oVcrOLouXg3aFJN651nvBGbu2sN1R4Aqq9QZWyMUWAfldLml_f3g026DhfBKQI7t07MCbGMSNwHx2NVXmuE8uxi7ZM2LZkFMWzbzxWQiMLdDt0tv7heulY4u5Rwm1dU4fsu9Lt7QQ31nUaALkqyixuMIul4CR5ubwVhob6LsTjo6GG2gE6um1vBd9KL5jitDHLhohxyFGtFeX-_dy9gYR2Nn8N_o5m00__y30000)

  - 1.1.1.3 **Get Charge Numbers (Truy xuất mã chi phí)**
    - **Mô tả**: Truy xuất danh sách mã chi phí liên quan đến dự án để tính toán chi phí lương.
    - **Tác nhân chính**: Payroll Manager.
    - **Tác nhân phụ**: ProjectManagementDatabase.
    - **Luồng sự kiện chính**:
      - Payroll Manager yêu cầu mã chi phí theo tiêu chí cụ thể.
      - Hệ thống truy vấn thông tin từ ProjectManagementDatabase.
      - Trả về danh sách mã chi phí cho Payroll Manager.
        
  - **Sở Đồ**:

  ![](https://www.planttext.com/api/plantuml/png/T90nQiCm58PtdU8dKplq0XvA1WzT10PdoVYgY4h5betqNF1OCkOK9OH081UmXmu-YKxGArHrsa8A7H__z_q_l8_nVHcOF7Tr9KXnur5GxvkgakJeINjGG255cn2hR4kEiVWcKFQ1TRsOaV8FufjdhVXIKcl7EJ4zKj0NMkP2519tzqdCi9vE7LGSZXtgQGzbB5epdS56Ds0xf-aMHJaRCi-mybsFbpWStBLoexnbxItTflxyPs3bux1F-FYA3Jc3CBqfSoN-TcTui77SkZGUnzs_-5AxpTVBFW400F__0m00)
  
#### 1.1.2. Ca sử dụng phụ trợ
  - **Validate Employee Information (Xác thực thông tin nhân viên)**
    - **Mô tả**: Kiểm tra tính hợp lệ của thông tin nhân viên trước khi thực hiện các tác vụ khác.
    - **Tác nhân chính**: Payroll Manager.
    - **Luồng sự kiện chính**:
      - Payroll Manager nhập thông tin nhân viên cần kiểm tra.
      - Hệ thống kiểm tra thông tin trong cơ sở dữ liệu.
      - Hệ thống trả về kết quả xác thực.
  - **Sở Đồ**:

  ![](https://www.planttext.com/api/plantuml/png/TD0nIiH06CNnVaxnIEy5KiWI8jX41h8N-CmEcy7aIvnyMJQbM7eA5Hl1Gh1AYYroaZc1Lp2pn4fi__nunVkUJfjEo4bVLueAQHmq3QwfgeoOziQ1EkXCjGknXMs91T4ga0-Tc3ewarpjIEYMEeFegcwhPZ06wPhE94sKqXakBXSSuwRquqSBAUSltaCiWylvXN6mypihdGUN9Z6shXzmyECR_sVJv7Tpw_pukk3f0NT-F0dk-n2EytE1sdAvpkeinhNrqsEOzDFJNnpoPw4sXdVXbny0003__mC0)
  
  - **Generate Payroll Reports (Tạo báo cáo tiền lương)**
    - **Mô tả**: Tạo báo cáo chi tiết tiền lương cho tất cả nhân viên.
    - **Tác nhân chính**: Payroll Manager.
    - **Luồng sự kiện chính**:
      - Payroll Manager yêu cầu tạo báo cáo.
      - Hệ thống thu thập dữ liệu từ các cơ sở dữ liệu liên quan.
      - Hệ thống tổng hợp và tạo báo cáo.
      - Báo cáo được xuất và cung cấp cho Payroll Manager.
  - **Sở Đồ**:

  ![](https://www.planttext.com/api/plantuml/png/ND2nQiCm40RWNK_napqluA64nAl1u2mTBx9n38hiogTGZvtw1DqRIYXaQMPho638U-W9-WgLWqDBbnESlkEE_zjT5YsJORjJWYJN1YbrfbOg8KrbOK0jqaGqWLIoQaWpPfD0rhLSx6OtaecSc3RK5h__yTIvYNWfH9fW_X1iXCVXP25z_sd1lZ_Ks0oXoB5mvTsBXhgUhmTTYZGRP-9bXBMn7Pwjxu-CtBilg21VRNY6ayQJ9JtXSS7QkpTTOklTHuFzyFv_pPqc4LOsm73BiVbpXTpMzoGmHI4MXSx7d7u0003__mC0)

## 2. Tài liệu giải thích lý do thiết kế các ca sử dụng cho hệ thống Payroll System
### 2.1. Giới thiệu
  - Hệ thống "Payroll System" được thiết kế để quản lý việc tính toán, gửi tiền lương, và cung cấp thông tin liên quan đến chi phí lương cho nhân viên trong tổ chức. Các ca sử dụng được xây dựng dựa trên:
    - Phân tích yêu cầu chức năng: Các tác vụ cần thiết mà hệ thống phải hỗ trợ.
    - Phân tích thành phần thiết kế: Dựa vào các hệ thống con như BankSystem, PrintService, và ProjectManagementDatabase.
Tối ưu hóa trải nghiệm người dùng: Đảm bảo người dùng, đặc biệt là Payroll Manager, có thể thực hiện các tác vụ một cách hiệu quả và chính xác.

### 2.2. Lý do thiết kế từng ca sử dụng
#### 2.2.1. Deposit Paycheck (Gửi tiền lương)
- Mục tiêu: Đảm bảo tiền lương của nhân viên được gửi chính xác và nhanh chóng vào tài khoản ngân hàng.
- Lý do thiết kế:
  - Đây là chức năng cốt lõi của hệ thống Payroll System, giúp giảm bớt thao tác thủ công và lỗi do con người.
  - Tích hợp với BankSystem để xử lý giao dịch là cần thiết để đảm bảo bảo mật và hiệu quả.
  - Quy trình này giúp Payroll Manager tập trung vào việc xác nhận thanh toán thay vì xử lý chi tiết từng giao dịch.
      
#### 2.2.2. Print Paycheck (In phiếu lương)
- Mục tiêu: Cung cấp phiếu lương dạng vật lý để lưu trữ hoặc trao đổi với nhân viên.
- Lý do thiết kế:
  - Một số tổ chức hoặc nhân viên vẫn cần phiếu lương in để đối chiếu hoặc lưu trữ.
  - Tích hợp với PrintService đảm bảo quy trình in phiếu lương được thực hiện tự động và chính xác.
  - Chức năng này cũng đáp ứng nhu cầu của những tổ chức chưa hoàn toàn số hóa quy trình quản lý nhân sự.
      
#### 2.2.3. Get Charge Numbers (Truy xuất mã chi phí)
- Mục tiêu: Giúp Payroll Manager truy cập nhanh mã chi phí dự án để tính toán lương.
- Lý do thiết kế:
  - Chức năng này hỗ trợ việc phân bổ chi phí lương cho các dự án khác nhau, đảm bảo minh bạch tài chính.
  - Tích hợp với ProjectManagementDatabase để lấy thông tin mã chi phí giúp tiết kiệm thời gian và giảm sai sót.
      
#### 2.2.4. Validate Employee Information (Xác thực thông tin nhân viên)
- Mục tiêu: Đảm bảo thông tin nhân viên là chính xác trước khi xử lý các tác vụ khác.
- Lý do thiết kế:
  - Thông tin nhân viên sai lệch có thể dẫn đến các vấn đề nghiêm trọng, như trả lương sai tài khoản hoặc sai số tiền.
  - Quy trình xác thực này giúp hệ thống trở nên đáng tin cậy và giảm thiểu rủi ro.
      
#### 2.2.5. Generate Payroll Reports (Tạo báo cáo tiền lương)
- Mục tiêu: Cung cấp báo cáo tổng hợp và chi tiết về tiền lương nhân viên.
- Lý do thiết kế:
  - Payroll Manager cần báo cáo này để phân tích, lập kế hoạch tài chính, và đáp ứng các yêu cầu kiểm toán.
  - Hệ thống tự động tổng hợp và xuất báo cáo giúp tiết kiệm thời gian và giảm bớt các công việc thủ công.
      
### 2.3. Thiết kế tổng thể
- Tác nhân chính: Payroll Manager
  - Đóng vai trò trung tâm trong việc tương tác với hệ thống để thực hiện các tác vụ như gửi lương, in phiếu lương, và tạo báo cáo.
      
- Tích hợp hệ thống con:
  - BankSystem: Đảm bảo giao dịch tài chính an toàn và nhanh chóng.
  - PrintService: Tự động hóa quy trình in ấn.
  - ProjectManagementDatabase: Cung cấp thông tin liên quan đến mã chi phí và dự án.
      
- Phân tách chức năng:
  - Các ca sử dụng được phân tách rõ ràng để đảm bảo mỗi chức năng có mục đích riêng, dễ bảo trì và mở rộng.
      
### 2.4. Lợi ích của thiết kế
  - **Đơn giản hóa quy trình làm việc**: Các ca sử dụng được thiết kế để Payroll Manager dễ dàng hoàn thành nhiệm vụ mà không cần hiểu sâu về các hệ thống con.
  - **Tính tự động hóa cao**: Tích hợp với các dịch vụ phụ trợ như BankSystem và PrintService giảm thiểu công việc thủ công và rủi ro sai sót.
  - **Khả năng mở rộng**: Hệ thống được thiết kế với các chức năng rõ ràng và độc lập, cho phép dễ dàng mở rộng để tích hợp thêm các tính năng mới trong tương lai.
  - **Bảo mật và độ tin cậy cao**: Tích hợp với các hệ thống con để xử lý các tác vụ quan trọng như giao dịch ngân hàng, đảm bảo tính bảo mật và chính xác.
