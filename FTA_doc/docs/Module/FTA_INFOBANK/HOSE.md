# HOSE INFOBANK

## Tổng quan
Module xử lý dữ liệu HOSE INFOBANK và cập nhật dữ liệu lên database:

* Thao tác xử lý:
    + Lấy dữ liệu từ folder chứa dữ liệu INFOBANK local
    + Check lịch sử file đã xử lý tìm dữ liệu mới
    + Biến đổi dữ liệu mới theo format setup 
    + Check và tìm lỗi của dữ liệu đã format 
    + Đẩy dữ liệu đã thỏa mãn lên SQL INFOBANK_database

## Tool, Design, layout

### Tool và data source:
    Tool:
        Python
        Power Automate

    Datasource:
        INFOBANK local_folder

    Database:
        InfoBankHSX


### Desgin
``` mermaid
flowchart LR

A[INFOBANK local_folder] -->|Python| B(INFOBANK_database)
B -->|SSMS,Excel| C[User]
A <--> |Power Automate| B
```

### Layouts

    HOSE_module
        Run application/
            [Automate]HSX_InfoB.bat
            [run]FTA_HSX_Info.py *        

        Module/
            System/
                .env
                Log_write_api.py
                sql_server_api.py
                HSX_Transform_api.py
            Format/
                BasicID_api.py
                Foreign_api.py
                Sessional_api.py
                OrderPlacement_api.py
        
        Log_history/
            log_HOSE/
                log_fileprocess.csv 
                log_filetrash.csv
                {date}_systemcheck.txt
                {date}_log_SyStoSQL_error.txt
            
* Run application
    * [run]FTA_HSX_Info.py *
        + Xử lý, kiểm tra và đẩy dữ liệu INFOBANK HSX lên SQL_database 
        + File chạy chính, và có thể sử dụng update theo ngày.

    * [Automate]HSX_InfoB.bat
        + File system sủ dụng trong power automate nhằm chạy tự động file [run]FTA_HSX_Info.py
* Module
    * System:
        * .env:
            + Chứa đường dẫn đến các folder chứa và lưu dữ liệu sau khi extract, process đại diện bằng các variable. 
            + Thông tin liên quan đến tài khoản kết nối SQL_server 
            + Khi cần thay đổi địa chỉ thử mục, đường dẫn vui lòng sửa trong file .env
            + Không thay đổi thứ tự các biến
            + folder_log: là biến tự động tạo theo vị trí của folder FTA_INFOBANK khi chạy vui lòng không thay đổi vị trí, số thứ tự của biến
    
        * Log_write_api.py:
            + Module dùng nhằm đọc và ghi kết quả chạy vào file txt dùng làm file log_history

        * sql_server_api.py:
            + Module kết nối và function đẩy dữ liệu lên SQL_server

        * HSX_Transform_api.py:
            + Module chứa function điều kiện lọc tên file
            + Xử lý dữ liệu dạng vòng lặp
            + Kiểm tra và xác định dữ liệu mới
            + Tạo DataFrame cho dữ liệu đã kiểm tra
    * Format:
        + 4 module đểu sử dụng nhắm format dữ liệu tương ứng với tên module:
            * BasicID_api.py
            * Foreign_api.py
            * Sessional_api.py
            * OrderPlacement_api.py

* log_HOSE
    * log_fileprocess.csv: Chứa tên file và sheet name những file đã xử lý
    * log_filetrash.csv: Chứa tên file và sheet name nhũng file không xử lý hoặc chưa xử lý
    * {date}_systemcheck.txt: Lịch sử kết quả chạy bào gòm cả error
    * {date}_log_SyStoSQL_error.txt: danh sách dữ liệu lỗi khi đẩy lên SQL_server