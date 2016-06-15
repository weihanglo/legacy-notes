# [Python] Date Quality Assurance

Data Format
-----------
- number
- string (should trimming all whitespace after upload?)
- datetime

Reference Data Schema
---------------------
- 選用 [TOML](https://github.com/toml-lang/toml) 作為 reference data 的交換格式
- 第一層: column
- 第二層: validator
- validator:
  - min/max
  - numeric/datetime range
  - datetime format (as POSIX format??)
  - enumerate
  - pair-wised data
- accepted error range


Frontend
--------
- 導引使用者建立reference data（類似google sheet）
- 可輸出自建的reference data（可再利用）
- validate upload file size
- Output View?????

Backend
-------
- 設計可參考 [Cerberus](http://cerberus.readthedocs.org)
- nginx 架站在 server1
- python+flask / R+shiny
