# PAYROLL SYSTEM USE CASE DESIGN SOLUTION

## 1. Create Administrative Report
#### Ở ca sử dụng này, ta phân tách thành hai biểu đồ Sequence: Tạo báo cáo và lưu báo cáo.
#### Các phần tử thiết kế: 
- Interface: PayrollAdministratorUI (UI) - Đây chính là interface mà người dùng tương tác trực tiếp.
- Hệ thống con (Subsystem):
  + ReportController (RC): Đây là một hệ thống con hoặc thành phần trung gian, xử lý logic nghiệp vụ và điều phối các thao tác giữa các thành phần khác (UI, ReportGenerator, ReportStorage).
  + ReportGenerator (RG): Đây cũng là một hệ thống con chuyên biệt để xử lý chức năng tạo báo cáo.
  + Report (R): Đây không phải interface hoặc hệ thống con, mà là một đối tượng dữ liệu (data object), được tạo ra trong quá trình xử lý và lưu trữ trong MySQL.
#### Biểu đồ Sequence Tạo báo cáo
![taoBC](https://www.planttext.com/api/plantuml/png/b991QiGW58RtESLRjZ1pWI1XGWgXcpO4vW1lp6kn9CRgoyAppQ97wXNwD9dIGXQj2n7z_j__5p-l7wV0w7cPnW8rpnuwZ7uUntgOZ3M1FQPD3D3LXHFGQEFGyYvsVaoWpA2KiKp-1JLLrIzTJsxstCoMavooTT_0RIWLbak8WMdQ5RPawJjItyAVXPc7lQ4KMJOSHLPqDHmhQL22f_U50ZUUa6crkDFUI2c3zuLq5AvlIj3xW5HAG5l2wvhuXd1qT83yvW-oUm2omxQOt3X7eYUSI0pQRF3p0f4yNzv8_yEa0NNCAJpnuksQOJFfSurqBZK64zo8SGifHoUnJ9_Y2m00__y30000)
### Biểu đồ Sequence Lưu báo cáo
![luuBC](https://www.planttext.com/api/plantuml/png/Z9E_QXj14CRxUuefBR1VG1p2GW7XnXO7xjoiLYDfpDtkUM_ES7MA56xiEWGIN8G40YbSwJ0kpkGzzWdo2fvTot-4LMYBOPdxPkQRttB_suV3YfNZkiWJfTawcAZ6sJmVpWeoLB5J8Qagc0oJKeIagLI6jyfEZu9G8gGf6KOtLne7Wusw34lhU6GDXtAChRCHl9mqhUffrLICnTR2CHfyjPIDOUV2g8Tj9qtHC74ZPSba20S3sQ0F3Yzgh7ZaK34-jzZJZcGfKht4M4Pmj5WosBcWwSFnujzVttuZkAZzwjP0tjr3q_skGVlLpnhOhtvOc7OIj8GpS-dRhnJk6fYYRjdzWJrkIjo7-2IVPF0-e9cjBqMPsmRnM1NOInAXB4wpKH_qTek9K0sASHyMpz1UD3lF4BwXm-Q8a-avwjsRR9AINe_NlhqXu83hrYpUcC3ZJSpfDQpBxhj0yUql1RpixaJAP29E8mdogmUEIwO7SKc7N3kpuJ7h1KpXks2QKLNcgbapoDRESfn7O-79nwIio7pxnO3qRp-7ERwzUcTHBosOZo-T7ChsuHTw0W00__y30000)

## 2. Create Employee Report
### Các phần tử thiết kế:
- Interface (EmployeeUI): Là phần giao diện người dùng, nơi nhân viên tương tác với hệ thống để cung cấp dữ liệu đầu vào (tiêu chí báo cáo, mã số công việc) và nhận kết quả đầu ra (báo cáo).
- Subsystem (EmployeeReportController): Xử lý các yêu cầu tạo báo cáo, điều phối giữa các hệ thống con như ReportGenerator và ReportStorage. Đây là nơi chứa các logic nghiệp vụ chính.
- Entity (ReportGenerator, Report, ReportStorage): Các thành phần này có chức năng tạo báo cáo và lưu trữ báo cáo. Report là kết quả dữ liệu, và ReportStorage lưu trữ báo cáo trong MySQL.
### Biểu đồ Sequence:
![BCNV](https://www.planttext.com/api/plantuml/png/Z9DBRi8m48RtFeN5YaZq0WWXn4EeYqfLGWym90DrSUpKdhJAsRheaNg5ZlCYBVJ1maAPxn_F_q_oyVQ-y0IEobmBICawkSaBRIj4KV1ZbQe23FKF7subUCddRAOCeJj0YlFvLJJ6mZfQMKFEQeqk23VnYfM-tFlA4-RVb8rYYmOTX4bO46-PHqEAggjmpVoE9DmAZbYJoH3DW60F7kMziq-OqXqOvdAkhvU1vdCswo3cHUTCtimvWgciWsikYV6vH4_ZI70sN6QZN4UJjIaunM4f6AVjdqY0xZrGLQ0SxIo1be-sT5w-MdV2J1uuXA8PRYGa_q9-t7szdCeZqWxyQMKpz7njgFB0DztTrDM6kZ1qfdoXeJfhUx9fSc4IDL_VuJqT2JOdshxnDinJhwrTUszq8iyANcQ0fp9r-0TvDk9gIbmwQELDFH9re0cyOAS8PeRBuD8NoKGUb4O3EKwajYcGiYOQfXKdOSNM_LV6RrS_TMhDGRayp3EEVbX1AAuQhkuoRZ9Ty16-nay0003__mC0)

## 3. Login
### Các phần tử thiết kế gồm:
- Interface (LoginPage): có thể coi là interface vì nó giao tiếp trực tiếp với người dùng và phản hồi theo các kết quả từ hệ thống.
- Subsystem (AuthService): là subsystem vì nó quản lý các nghiệp vụ xác thực và không tương tác trực tiếp với người dùng.
- DataBase: nơi lưu trữ dữ liệu người dùng - sử dụng MySQL
### Biều đồ Sequence:
![loginSequence](https://www.planttext.com/api/plantuml/png/T971QW8n443l-OhWoONw0uk8scsXu47OjlSncMeWcompinQ_hOT-Kd-X4rS4fTt37f8tRnxav-jxoG8aGnSDECbatnZ9z7eKNEWXYPriyZwaBUnnOe7jPcldyv04wGCSBXQtx6gGGujq36waLwtIFEpun8BTFTs0m0vuH9lr7MfAYfqjT6LjSu_f6ZAjRkvqg0jolfqEUfwWmmVR0_Dd9byPJLPorTRs235u47maz9WaGEG_9pHR9vfrRVSePLKflPALqTRPHKae0wKhKnc8OWE_bqt6wbTSbz1O4jl1EUHnRtKcnhwYA3eV29syvWRuiCj0NfqO6LNwaex_QfyXH2pilT47xYESdeWo5LNoPgc_ykA_0000__y30000)

## 4. Maintain Employee Information 
### Các phần tử thiết kế gồm:
- Interface (EmployeeUI): là interface vì nó giao tiếp trực tiếp với người dùng, nhận thông tin đầu vào và hiển thị kết quả.
- Subsystem (EmployeeController): Là hệ thống con chịu trách nhiệm xử lý các yêu cầu từ giao diện người dùng và thực thi các nghiệp vụ như thêm, sửa hoặc xóa thông tin nhân viên.
- DataBase: nơi lưu trữ dữ liệu nhân viên - sử dụng MySQL
### Biểu đồ Sequence:
![MEI](https://www.planttext.com/api/plantuml/png/Z9J1Jjmm48RlUOgvaPMM5rYX5MYp1ovLfNObhiOUDXQE4sm7TP-W9uHwxA42sXiIQgNsKYB4mHNluIVW5HWdNRGiks9pSABnpFp_Pu_osDplMiUCgmkLCEvA0nEB9gae9Bcic7OmBYfLpX0d-y0iqBgp8xL3SyGu3eShKqUbTgPK2aqi6O-enDQ7TcOT5bGYc6E7pE9pVZOFnEmiIRRWtVJXLsY-IH3-hvv24PeBS8RHvqaTRdzeKFuENEx_KCH93JhttpMSId-jaqW0sqEoEe2oGZrNUS-ccFPMTETvQCuqvFvIv_3lIsY-KZ2bxjT57sneRbWVFldVR56bbz19aCXuD0239pLQjyUTB7NAsbSVS06EL9boi2V4CtC2z6p1nwYoXWHE_MK9_E4gchW04PgVe6HeFjTjCPrhD90DW0anRvk-bEr43lmLfyRXzaP3Y_L2nNNWF5he6cUm_H-Db_f8ceACfxq5qNYqGjfAiHbjVQWvHsif0nLTugIY2yPbq16fLvq9juwNXYPUnzl0TIknCJDVqduBjoDOHzpjBa5dgF0rzC7IrC0nZTgvt0HHj0rV8UwBLO3jT6u0rhbS1zRjBe1faUpI4dyEJm000F__0m00)

## 5. Maintain Purchase Order
### Các phần tử thiết kế gồm:
- Interface (CommissionedEmployeeInterface): Giao diện của nhân viên để tương tác với hệ thống.
- Subsystem (MaintainPurchaseOrderController): Là hệ thống con chịu trách nhiệm xử lý các yêu cầu từ giao diện người dùng và thực thi các nghiệp vụ như thêm, sửa hoặc xóa thông tin đơn hàng.
- PurchaseOrderDataBase: nơi lưu trữ dữ liệu đơn hàng - sử dụng MySQL
### Biểu đồ Sequence:
![MPO](https://www.planttext.com/api/plantuml/png/T5D1Jjmm5Dtd57_78D4B83HYcbHq5WM4kkZMs1zYrR63_GsQDOik40jkmBGB92HMT9LPi4ZLU-G4lK9_CXbew10fSUIyz_pUi_DdyRGRI7YAXKc49ESXTKMXGz3EelfGbCRD49Da0_QqSA1qi_XcuRo-XPpVWFXvOqz1EfkKBAEbBeMbjI9JI-XFX4GG0IQmiwDN4-FnWFn9y1U-3wENkGXuu1Nwr5dopXZqBJrbUeZ7OHO82wOhGUAOeJ3WPAjPPcJCMA6Om87sy_exHz7rlGN9EQujn-6CLCzbiYu0l1kpxsq6EnTm8ec_ZZQxRfh5WuPPVHz1DjLTV17gggAy_iabaRRmw-Rtt49UtzhJPD8AfYnOUYSnX5vHTCCMk2u2SXCcy2h247nkghaRQ01VQQkJjSOy2bf67mtPBInRBUUHehSTR9ejWTDiyqMgpHXoT_4V0WrtcJRLGmasvu7UjdA29FDEuFtizIBhZFHEH-fVnyzgiLJ3ODDigvzKpndHgcLBN-f7yROpXGPVQVNS3VZ8n_lITgVw2husrHF1MMog7_rMhJiJowgEC4H38zyDl5cxBDZ-Kdy1003__mC0)

## 6. Run Payroll
### Các phần tử thiết kế gồm:
- Interface (PayrollInterface): Giao diện người dùng để yêu cầu và hiển thị bảng lương.
- Interface (BankSystemInterface): Giao diện để tương tác với hệ thống ngân hàng.
- Subsystem (RunPayrollController): Subsystem xử lý quy trình tính bảng lương và tương tác với các thành phần khác.
- PurchaseOrderDataBase: lưu trữ dữ liệu nhân viên và bảng lương, thực hiện các thao tác truy vấn và cập nhật - sử dụng MySQL
### Biểu đồ Sequence:
![RP](https://www.planttext.com/api/plantuml/png/b5HBRi8m4Dtd55x2eXT02D525smGAk80WpEq5lxL7bFbR5tqIBr2xM28476Rhc9vtdipy_oKxy-lkITm59IiW9DnREVHLJPU2IuiQ68RQ9oHSgK9tG4uikbKNCwpsGtq2VHnstX2DGJz4dJMNXXDwOikmdtO-rOZmciWs8D7jio7gahpiOVP_LWJvl0zeATS6OshEqpazNQTiDQ5NDWumz7xAD0BZYANSIBn5UbPMMaQn7Gx6hFgMYstSqZ1wLjYiLj1WuFaGG9Xjt19eSUiMdWheScLRL0AN5FmhFKyUlHcFd9vYGH29ekk3rAO4gnrvZHWnWB_X4uSchks9PM-24wOq8B4sIc5cYA_3_UBrKOVX5EPlZgh2QF_lqvq-VZeSyAm7fQnOElkcRS45985WsEsQ-cBymv_pTqJ5MseUuA5YQ75B38iB1rbdPG4lymmHrsdFyyF0000__y30000)

## 7. Select Payment
### Các phần tử thiết kế gồm:
- Interface (PaymentInterface): Đây là giao diện mà người dùng (User) tương tác với hệ thống để chọn phương thức thanh toán.
- Subsystem (PaymentController): Là bộ điều khiển chịu trách nhiệm xử lý logic nghiệp vụ của quy trình chọn phương thức thanh toán. 
- Subsystem (PickUpSystem): Thực hiện việc lên lịch thanh toán theo phương thức Pick-up.
- Subsystem (MailSystem): Thực hiện việc gửi thanh toán qua thư điện tử. 
- Subsystem (BankSystem): Thực hiện thanh toán qua chuyển khoản ngân hàng (Direct Deposit). 
- DataBase: Database lưu trữ thông tin về phương thức thanh toán mà người dùng đã chọn và thực hiện các thao tác cập nhật khi người dùng chọn phương thức thanh toán - sử dụng MySQL.
### Biểu đồ Sequence:
![SP](https://www.planttext.com/api/plantuml/png/d9H1RiCW44NtFWNAgbta0b5aHQqtNKI9LEK014za50m8ngfojYvwf5wXO1CPdDYDiqFmt_3d3_Rlzy_68ZNOr2AZ39KX1micqswBCwwfHBAdbneaVaW4Sw8Co7hDh-iyloTzLnAD4WACqzhcQ2yMeHvgEJiVz6TxD27RKYx-5RrHURuhAYdI8xL0Yh38CjyVMUQtRQs81G4Cmy4Mi5Bbosjs8-pXg557L-ehxEyqSYLj3qT2HxSM0j2cu9iiG2lB8tJAAQkKij31Sons3Gwmr5mo5uUm2if6H7V5voFtC2LFtDH16YgKOpTUP-F0Hhk9GJg1XI-pRFJYaKXyahC3IQ7KNFJ-LeHBZjmPz9j1xRX8Cfr7A-oOfuBm_4Cf5DoujiABcXt729rwZJwvFfSX6Occaqd0lL4Ch7t-mNJLI2Zd4zk0BFqlxWy00F__0m00)

## 8. Maintain Timecard
### Các phần tử thiết kế gồm:
- Interface (TimecardInterface): Giao diện người dùng cho việc tương tác với thời gian làm việc.
- Subsystem (TimecardController): Bộ điều khiển xử lý các yêu cầu của người dùng về thời gian làm việc. 
- DataBase: Lưu trữ dữ liệu về thời gian làm việc của nhân viên. - sử dụng MySQL.
### Biểu đồ Sequence:
![MT](https://www.planttext.com/api/plantuml/png/d9H1ReD034Ntd6AMxQ8NYA8e4ksYKdTf3k20IKOQPgXjKd6sBdgaNg4pK1AW2O7iHjZ_V_inyFFrlMO1aZ8t4IJYI6qPAIhy8vte0goeTvrZ0fI-Ma7A846rNEhsl5fTx8sT5NB68FbcBdTSiM3kcrCGs06ZUluxH548L4-h2paBPTnUsuV7w7-j8-Y4BTGHZFOX65nZmXIjQ33SyUYqUvDsZY15qbdL5vtAr_88fIHx5cq4fBmUTsd9L7DXe7eBkvxaerW8FqfaQKkp06KeoQ6jXFMceDcZz2HXkCbm9eMDW1deHycKHNZveVBYtQjPP0RQgMmOZhYjfUbWqfjy4cSpJNbRQrnc8UA3-no4tqBaFyTSttTt-j8vW3QriZ_bN3or1xDszfvRT5R7ZIr8unIjqQRX__SB003__mC0)
