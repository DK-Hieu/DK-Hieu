# FTA_EOD: FTA Intraday price data

## Tổng quan
Trích xuất và lưu dữ liệu giá giao dịch Intraday thông qua Fdata và Amibroker. Thao tác gồm:

* Dữ liệu EOD từ Fdata sẽ được trích xuất thành các file csv riêng lẻ thông qua fucntion trong AmiBroker.
* Sử dụng Python nhằm nối và format lại định dạng của dữ liệu, sau đó đẩy dữ liệu lên SQL_server. 
* Các thao tác trên sẽ được thực hiện auto bằng Power Automate.

## Tool, Design, Layouts

### Tool và data source:
    Tool:
        Power automate 
        Amibroker 
        Python 
        Fdata

    Datasource:
        Fdata

    Database:
        Fdata.EOD

### Design:
``` mermaid
flowchart LR

A[Fdata] -->B(Amibroker)
B --> |Python| C[Fdata.EOD]
C -->|SSMS,Excel| D[User]
A <--> |Power Automate| C
```

### Layouts

    EOD
        Run application/
            [run]EOD_fdata.py

        Module/
            .env # Chứa variable trong file python
            sqlserver_api.py # Module kết nối với sql_server

        Log_history/
            log.txt
            runtime.txt

* .env: 
    + Chứa đường dẫn đến các folder chứa và lưu dữ liệu sau khi extract, process đại diện bằng các variable. 
    + Thông tin liên quan đến tài khoản kết nối SQL_server 
    + Khi cần thay đổi địa chỉ thử mục, đường dẫn vui lòng sửa trong file .env
    + Không thay đổi thứ tự các biến
* sqlserver_api.py: 
    + Module được thiết kế nhằm kết nối python với SQL server và chứa một số fuction cơ ban phục vụ truy vấn SQL trên python
    + Có thể bô sung thêm các function trong quá trình làm việc.

