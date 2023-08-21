# Electricity_dailyouput

## Tổng quan:
Trích xuất và lưu dữ liệu dữ liệu từ Website của EVN tại Server của FTA => FFA_database

* Các thao tác bao gồm:
    + Crawl dữ liệu, format, và đẩy dũ liệu lên SQL_server bằng Python
    + Các thao tác sẽ được thực hiện auto bằng Power automate

## Tool, Design, Layouts

### Tool và data source
    Tool:
        Python
        Power automate
    
    Datasource:
        Web
    
    Database:
        FFA.Eletrictiy_Dailyoutput

### Design
``` mermaid
graph LR
  A[EVN Website] --> |Crawl and Transform: Python| B[Database];
  B -->|SQL_Query:SSMS,Excel| C[User];
  A <--> |Auto Flow: Power Automate| B
```

### Layouts
    Electricity_FFA
        Main file/
            NamDD_request_ver2py
            
        Folder/
            backup 
            log_hist 

* NamDD_request_ver2py: File chạy dữ liệu hàng ngày
* backup: Chứa file backup dữ liệu đã lấy trước khi đẩy dữ liệu vào Database 
* log_hist: Chứa file ghi lại lịch sử chạy chương trình.

