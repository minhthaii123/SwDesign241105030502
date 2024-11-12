# Lab 3. Identify design elements

## 1. Subsystem context diagrams
  ### 1.1 Biểu đồ ngữ cảnh của hệ thống con PrintService và giải thích
- **Biểu đồ ngữ cảnh của hệ thống con PrintService**
  
  ![](https://www.planttext.com/api/plantuml/png/j95D3e8m44RtFKMNciW5Y24cnWKx8YUePP29fIN3-DEpkV18Ni5Y322oTTLClpVp9ktp_jYqh8ZFjH5AioEPAK_EcAspt9r0Sht-54aYm3Aobsb6Q3a7kg260AIMWKgbOK0cH7u-jBvbg4FWRdx4AQyhqAV0xDutGxIh6-CyG6fBHxLYT5Q8t_qYmcF5KJBPAfPDLmO-DzWiL2-AU-TAmaWHWXdZKdoFxMt_aOblMU6kjdCDu_R0X701MG0hDErymypiSI-ENtG3jkZ-_mK00F__0m00)

- **Giải thích**
    -  PayrollController là một lớp actor, đại diện cho phần điều khiển.
    -  IPrintService là một giao diện (Interface).
    -  PrintService là một hệ thống con (Subsystem Proxy).
    -  Paycheck và EmployeeInformation được định nghĩa là các lớp kiểu entity:
       - entity Paycheck <<Entity>>: Tạo lớp entity cho phiếu lương.
       - entity EmployeeInformation: Tạo lớp entity cho thông tin nhân viên.

  ### 1.1 Biểu đồ ngữ cảnh của hệ thống con PrintService và giải thích
- **Biểu đồ ngữ cảnh của hệ thống con ProjectManagementDatabase subsystems**
  
  ![](https://www.planttext.com/api/plantuml/png/j9AnJiCm48PtFyLjW4HV8AgYIfIXGoK4Jt1nhebHQaVsfMhcYWTXO2XCI4naO8Xua3m1hu1BqmQ85B4mMRxxVFztaZ-gjubZj5miCu6IZOKhQsv9yeNHR4sMaONnkBs4eI3DYakOjTGSDIQqzDKfCaReoDCppMGNAAdZX_2R8dAbOrhkg7NPU-IHowz2hpCbHfMvxu3ewu-iIb8UXKFI0JXSKTi_pTlWu11q3ldFnE2NmfaO67uK-CzySGBpzwq2hXyroBJU6eXKKsqAYFrnfy4rrJEmBKfO5yth0mEdzOjEW9K6RgedaFMzz4MFxO-D65YfsyQxN1DRHIiwM4Ayj_hRW6wdtXoNarGB9P6LqKw82UbuzrC_0G00__y30000)

- **Giải thích**
    -  ProjectController khởi chạy các thao tác quản lý dự án thông qua IProjectManagementDatabase.
    -  IProjectManagementDatabase chuyển yêu cầu tới ProjectManagementDatabase để lưu trữ hoặc cập nhật dự án.
    -  ProjectManagementDatabase truy xuất thông tin từ Project và ProjectDetails để hoàn tất các thao tác.
  
## 2. Analysis class to design element map

## 3. Design element to owning package map

## 4. Architectural layers and their dependencies


