# INFOBANK freefloat, CommonStock, OrderFlow

## Tổng quan
Module xử lý dữ liệu freefloat, CommonStock, OrderFlow và cập nhật dữ liệu lên database:

* Thao tác xử lý:
    + Lấy dữ liệu từ folder local chứa dữ liệu 
    + Biến đổi dữ liệu mới theo format setup
    + Đẩy dữ liệu đã thỏa mãn lên SQL INFOBANK_database

## Tool, Design, layout

### Tool và data source:
    Tool:
        Python
        Power Automate

    Datasource:
       local folder

    Database:
        InfoBank

### Desgin
``` mermaid
flowchart LR

A[local folder] -->|Python| B(INFOBANK_database)
B -->|SSMS,Excel| C[User]
A <--> |Power Automate| B
```

### Layouts

    HOSE_module
        Run application/
            [run]freefloat.py
            [run]FTA_Common_InfoB.py
            [run]orderflow.py

* Run application
    * [run]freefloat.py
        + Xử lý và đẩy dữ liệu Freefloat lên SQL_database
        + Dữ liệu hiện không có chức năng 
            + Update theo ngày
            + Check file đã chạy
        + Dữ liệu có chức năng:
            + Xử lý toàn bộ dữ liệu có trong dữ liệu gốc
            + Phù hợp dùng cho restore dữ liệu
    * [run]FTA_Common_InfoB.py
        + Xử lý và đẩy dữ liệu CommonStock lên SQL_database
        + Dữ liệu hiện không có chức năng 
            + Update theo ngày
            + Check file đã chạy
        + Dữ liệu có chức năng:
            + Xử lý toàn bộ dữ liệu có trong dữ liệu gốc
            + Phù hợp dùng cho restore dữ liệu
    * [run]orderflow.py
        + Xử lý và đẩy dữ liệu CommonStock lên SQL_database
        + Dữ liệu hiện không có chức năng 
            + Update theo ngày
            + Check file đã chạy
        + Dữ liệu có chức năng:
            + Xử lý toàn bộ dữ liệu có trong dữ liệu gốc
            + Phù hợp dùng cho restore dữ liệu