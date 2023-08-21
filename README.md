# FTA_database Project

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Tổng quan

* Xây dựng Database chứa dữ liệu chung phục vụ chuyên viên phân tích
* Chuẩn hóa dữ liệu phục vụ quá trình chạy  model trong tương lai


## Project tool + design + layout

### Project Design:
``` mermaid
graph LR
  A[Data source] --> |Transform: Python| B[Database];
  B -->|SQL_Query:SSMS| C[User];
  A <--> |Auto Flow: Power Automate| B
```
### Project Tool: 
* Database: SQL Server 
* SQL: SSMS 
* Python: 3.9, 3.10, 3.11 
* Source-code Editor: VScode, CMD, PowerShell
* Auto flow: Power Automate
* Other: AmiBroker, Fdata (Filada data), Onedrive pc

### Project layout
    FTA_sourcecode
      module/
          Electricity_FTA
          EOD
          INFOBANK_module
          Onedrive_downbycopy

      Database_design/
          fta_sample2_DB_code.sql
          fta_DB_ERDigram.vuerd.json
          
      Python_evne/
          FTA_env.yaml
          requirement.txt
