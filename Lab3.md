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

  ### 1.1 Biểu đồ ngữ cảnh của hệ thống con  ProjectManagementDatabase subsystems và giải thích
- **Biểu đồ ngữ cảnh của hệ thống con ProjectManagementDatabase subsystems**
  
  ![](https://www.planttext.com/api/plantuml/png/j9AnJiCm48PtFyLjW4HV8AgYIfIXGoK4Jt1nhebHQaVsfMhcYWTXO2XCI4naO8Xua3m1hu1BqmQ85B4mMRxxVFztaZ-gjubZj5miCu6IZOKhQsv9yeNHR4sMaONnkBs4eI3DYakOjTGSDIQqzDKfCaReoDCppMGNAAdZX_2R8dAbOrhkg7NPU-IHowz2hpCbHfMvxu3ewu-iIb8UXKFI0JXSKTi_pTlWu11q3ldFnE2NmfaO67uK-CzySGBpzwq2hXyroBJU6eXKKsqAYFrnfy4rrJEmBKfO5yth0mEdzOjEW9K6RgedaFMzz4MFxO-D65YfsyQxN1DRHIiwM4Ayj_hRW6wdtXoNarGB9P6LqKw82UbuzrC_0G00__y30000)

- **Giải thích**
    -  ProjectController khởi chạy các thao tác quản lý dự án thông qua IProjectManagementDatabase.
    -  IProjectManagementDatabase chuyển yêu cầu tới ProjectManagementDatabase để lưu trữ hoặc cập nhật dự án.
    -  ProjectManagementDatabase truy xuất thông tin từ Project và ProjectDetails để hoàn tất các thao tác.
  
## 2. Analysis class to design element map
# BankSystem

| **Annlysis class**    | **Design Element**      |
|------------------------|-------------------------|
| IBankSystem           | IBankSystem       |
| PayrollController     | PayrollController |
| BankSystem            | BankSystem        |
| Paycheck              | Paycheck         |
| BankInformation       | BankInformation   |

# PrintService

| **Annlysis class**    | **Design Element**      |
|------------------------|-------------------------|
| IPrintService          |    IPrintService         |
| PayrollController      | PayrollController        |
| PrintService           | PrintService             |
| Paycheck               | Paycheck                 |
| EmployeeInformation    | EmployeeInformation      |

# ProjectManagementDatabase

| **Annlysis class**    | **Design Element**      |
|------------------------|-------------------------|
| IProjectManagementDatabase   | IProjectManagementDatabase    |
| ProjectController            | ProjectController             |
| ProjectManagementDatabase    | ProjectManagementDatabase     |
| Project                      | Project                       |
| ProjectDetails               | ProjectDetails                | 

## 3. Design element to owning package map
# BankSystem

| **Design Element**    | **Owning Package**      |
|------------------------|-------------------------|
| IBankSystem           | FinancialServices      |
| PayrollController     | PayrollManagement      |
| BankSystem            | FinancialServices      |
| Paycheck              | EntityManagement       |
| BankInformation       | EntityManagement       |

# PrintService
| **Design Element**       | **Owning Package**     |
|---------------------------|------------------------|
| IPrintService             | DocumentServices      |
| PayrollController         | PayrollManagement     |
| PrintService              | DocumentServices      |
| Paycheck                  | EntityManagement      |
| EmployeeInformation       | EntityManagement      |

# ProjectManagementDatabase
| **Design Element**          | **Owning Package**      |
|------------------------------|-------------------------|
| IProjectManagementDatabase   | ProjectServices        |
| ProjectController            | ProjectManagement      |
| ProjectManagementDatabase    | ProjectServices        |
| Project                      | EntityManagement       |
| ProjectDetails               | EntityManagement       |

## 4. Architectural layers and their dependencies

  ###### system
  ![](https://www.planttext.com/api/plantuml/png/R99FIiD058VtESMZ-rx0XTXQa4B1Wjr95w_JSJ8qVLFcZpI8QnTUGWKH1A62gmRf8j1xv0HUmQHgCwcJJKWot_VUxqU-iis9iQYjcoVH0jaC1OVMK7F3oQALYc20ATSjk8cWl2w7c6gL9AUAR7NdUWnee7wCRgFQqtL64ZS61af8Tc3g8iqkkBwMZ8yRL9yi5peqV8UanlBvKAjbsiHwQ14wZEtcDR2HHZB8Ac6lS_wVcg3XVa0MSpQ34KwIShFzu3vTAJt_MUltMocgaqExVGnUA3Y2io9xav3chmvOiNvni2nVG99_Gh9TRHz9HFxvFLyd33c4H0NJ8hjdCP38dmZY_E5FvQ5XtIWkidS6iIooE_9TGRxPN8aFjYi7Diu_I82LJS71uOe_R3DWM9Ihh3TktqZ84gw_IgDT2ajNh9-jx_HhEU4qhNxkRm000F__0m00)
 ###### ProjectManagementDatabase subsystems
 ![](https://www.planttext.com/api/plantuml/png/V9AnIWD148RxUuh1HYr2UWj9D292m4ZIYSLcirnMDtDnTpRa4ElKrZO64I4WKUnoI8e3tsEVm5TmBq6IImwts6Rd--URON-IUSKGqsHxAkWpViD20JiDBOn0OYGZX3gBXTw1km3ykMpew5fmEewGTAIKq5V1VR0YZwoHA8o1UXHANimsXHv8BlBW6P88TL77ao49ZKmrOqEYvpE6SHwjCM9GvNpHjgXXhNg-JRIP4Pk5q69jvSLoi20cbVbxyZ6xS64PGjSb8mYbIwOCU3hcG6xsYc6mjI4ebGuXFpiSmAbBtYJ4wSG2zw25M-jcpmWg_OAEIpuW7MEmGQq5-PbyIFtxtPPRsiOmzFGBPUGKb9SQsNzJ2fQQEKaM0Katc_TXu997kHoI_Fs08RJJ2GA6KVeaOGzzbLTFF_U3DQKiUsERFdTXEF22MCwCjymsoVpE2m9uLouzQPLL4TZ9Vl4l0000__y30000)
###### PrintService
 ![](https://www.planttext.com/api/plantuml/png/R9C_IyD06CRtV8gNBkfGt1sazG-Y5AoqWY8Eb-jvFRo-2NUNqY3E7PoSNNGeGa4gwDGW7G9-Ztm2luANjgQcIOORmlDxtkUUb_k9PZLjY391Jpe-eRU4CwWq5TCC3J72GsYGaAaAt3bWlwjppTGn6gPk26NNphspekg-BmKjWvfAe6anrHSfi_grxw5HdfHCvPts0YsGQGqDZmjQPjPK7hK2WJop_M-G9kIgBChXm6P78bkXDgndRGPX7ZqWXa2Tqlduuk23-cbHxnBDyh8JpuKsSUKYrmQS1GIXcqH3u2A99WHe_4B19DDNv4wkKwXMTs6j7TY1eoHw4n36um2efG8GwAohCdBPYSKkLq0dYHve5_f9DChWFs565dgr7XTsDCZuAwEAeeotzLYYyVqUWEd6dyZ122mTLxA8z9g2U1P9fZC_JVea5gKPUpvQCpSU8o3tucS1csXLzdBnnvQJpKwTrpUm3BJTLa48Wo2PZanQnWIaNSLmtcIDOITz0Ry0003__mC0)


