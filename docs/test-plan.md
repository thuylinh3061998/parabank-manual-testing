# Test Plan – ParaBank Transfer Funds & Bill Pay

| Mục | Nội dung |
|---|---|
| Dự án | ParaBank Banking Test Project (personal) |
| Phiên bản tài liệu | 1.0 – 30/10/2026 |
| Test Lead | Mia Pham |
| Tài liệu liên quan | `docs/requirements.md` |

---

## 1. Mục tiêu
Xác nhận chức năng Chuyển tiền (Transfer Funds) và Thanh toán hóa đơn (Bill Pay)
hoạt động đúng, an toàn về số dư, và xử lý dữ liệu không hợp lệ đúng cách
trước khi phát hành.

## 2. Phạm vi
**Trong phạm vi:**
- Transfer Funds
- Bill Pay
- Accounts Overview (kiểm tra số dư trước/sau)
- Find Transactions (kiểm tra lịch sử giao dịch)

**Ngoài phạm vi:**
- Request Loan, Admin Page, Update Contact Info
- Performance test, security test chuyên sâu

## 3. Loại test
| Loại | Mô tả |
|---|---|
| Functional | Luồng hợp lệ hoạt động đúng |
| Negative | Dữ liệu sai: chữ, để trống, số âm, ký tự đặc biệt |
| Boundary | Giá trị biên: 0, 0.01, bằng số dư, số dư + 0.01 |
| Data integrity | Số dư 2 tài khoản trước/sau, tổng không đổi, lịch sử giao dịch đúng |
| UI trên mobile browser | Hiển thị và thao tác trên màn hình điện thoại |
| Regression | Chạy lại các case chính sau khi bug được sửa |

## 4. Kỹ thuật thiết kế test case
- Phân tích giá trị biên (Boundary Value Analysis)
- Phân vùng tương đương (Equivalence Partitioning)
- Bảng quyết định (Decision Table)
- Đoán lỗi (Error Guessing)

## 5. Môi trường
| Thành phần | Chi tiết |
|---|---|
| Ứng dụng | https://parabank.parasoft.com |
| Môi trường dự phòng | ParaBank chạy local bằng Docker |
| Trình duyệt | Chrome (Windows 11) |
| Mobile | Chrome DevTools – giả lập màn hình điện thoại |
| Quản lý bug | Jira Cloud – project PBT |
| Lưu tài liệu | GitHub – repo parabank-manual-testing |

## 6. Dữ liệu test
- 1 user test, 2 tài khoản (Checking)
- Ghi lại số dư của cả 2 tài khoản trước và sau mỗi test case
- Không dùng thông tin cá nhân thật

## 7. Tiêu chí bắt đầu / kết thúc
**Bắt đầu (Entry):**
- Môi trường truy cập được, đăng nhập được
- Đã có tài liệu yêu cầu và test case được review

**Kết thúc (Exit):**
- 100% test case đã được chạy
- Không còn bug Critical / High ở trạng thái mở
- Đã có test summary report

**Tạm dừng (Suspension):**
- Môi trường không truy cập được > 2 giờ → chuyển sang môi trường dự phòng

## 8. Phân công (nhóm giả định 5 người)
| Thành viên | Phụ trách | Số case dự kiến |
|---|---|---|
| Test Lead (Mia) | Lập kế hoạch, review test case, tổng hợp báo cáo, họp 15 phút mỗi sáng | – |
| Tester A | Transfer Funds – luồng hợp lệ | 5 |
| Tester B | Transfer Funds – negative & boundary | 8 |
| Tester C | Bill Pay | 7 |
| Tester D | Mobile browser | 3 |
| Tester E | Regression: Accounts Overview, Find Transactions | 2 |

## 9. Lịch trình
| Ngày | Hoạt động | Người thực hiện |
|---|---|---|
| D1 | Phân tích yêu cầu, gửi câu hỏi cho BA | Lead |
| D2 | Viết test plan, viết test case | Lead, A–E |
| D3 | Review test case | Lead |
| D4 | Chạy test, ghi bug | A–E |
| D5 | Retest, regression, test summary report | Lead, E |

## 10. Rủi ro và phương án xử lý
| Rủi ro | Khả năng | Ảnh hưởng | Phương án |
|---|---|---|---|
| Môi trường demo dùng chung bị lỗi / reset dữ liệu | Cao (đã xảy ra 30/10) | Cao | Chạy ParaBank local bằng Docker; ghi lại số dư sau mỗi case |
| Không có spec gốc | Cao | Trung bình | Viết yêu cầu ngược, gửi câu hỏi làm rõ cho BA |
| Thiếu thiết bị mobile thật | Trung bình | Thấp | Dùng giả lập; ghi rõ giới hạn trong báo cáo |

## 11. Sản phẩm bàn giao
- `docs/requirements.md` – yêu cầu ngược + câu hỏi làm rõ
- `docs/test-plan.md` – tài liệu này
- `test-cases/testcases.xlsx` – bộ test case
- Bug report trên Jira (project PBT)
- `reports/test-summary.md` – báo cáo tổng kết
- `reports/rca-bug-xx.md` – phân tích nguyên nhân gốc
