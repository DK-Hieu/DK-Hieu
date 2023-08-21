# Onedrive_downbycopy

## Tổng quan
Module sử dụng nhằm tự động download dữ liệu INFOBANK từ Sharepoint về máy tính local thông qua việc đồng bộ folder INFOBANK trong máy local và folder INFOBANK trong ổ cứng ảo Onedrive trên máy local. Các thao tác thực hiện sẽ được tự động trên Power automate.\
Thao tác thực hiện:

* Cài đặt phần mềm:
    + Cài đặt, đăng nhập Sharepoint bằng Onedrive PC trên máy local
    + Tạo shortcut folder INFOBANK từ Sharepoint về Onedrive PC và tiến hành đồng bộ.
    * Copy file từ folder INFOBANK Onedrive sang INFOBANK local.

## Tool, design, layouts

### Tool và data source
    Tool:
        Onedrive PC
        Python 
        Automate

    Datasource:
        Sharepoint

### Design

``` mermaid
graph LR
  A[Sharepoint] --> |Syncing data: Onedrive PC| B[Onedrive PC];
  B -->|Check and copy: Python| C[INFOBANK local folder];
  B <--> |Auto Flow: Power Automate| C
```

### Layouts

    Onedrive_downbycopy

        Run application/
            DownFileFormOneDrivePC.py

        Module/
            .env

* .env: 
    + Chứa đường dẫn đến các folder chứa và lưu dữ liệu sau khi extract, process đại diện bằng các variable. 
    + Thông tin liên quan đến tài khoản kết nối SQL_server 
    + Khi cần thay đổi địa chỉ thử mục, đường dẫn vui lòng sửa trong file .env
    + Không thay đổi thứ tự các biến

