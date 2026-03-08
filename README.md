# Website Performance Testing using Apache JMeter

## 1. Giới thiệu
Bài thực hành này sử dụng Apache JMeter để kiểm thử hiệu suất của một website.  
Mục tiêu là mô phỏng nhiều người dùng truy cập đồng thời vào hệ thống và đo lường các chỉ số hiệu năng như:

- Response Time (thời gian phản hồi)
- Throughput (số request xử lý mỗi phút)
- Error Rate (tỷ lệ lỗi)

---

## 2. Công cụ sử dụng

- Apache JMeter 5.6.3
- Java
- GitHub (lưu trữ kết quả kiểm thử)

---

## 3. Kịch bản kiểm thử

### Thread Group 1 – Kịch bản cơ bản
- Number of Threads (Users): 10
- Loop Count: 5
- Hành vi:
  - Gửi HTTP GET request tới **trang chủ** của website.

---

### Thread Group 2 – Kịch bản tải nặng
- Number of Threads: 50
- Ramp-up Period: 30 giây
- Hành vi:
  - Gửi HTTP GET request tới:
    - Trang chủ
    - API post

---

### Thread Group 3 – Kịch bản tùy chỉnh
- Number of Threads: 20
- Duration: 60 giây
- Hành vi:
  - Gửi HTTP POST request tới endpoint `/posts`.

---

## 4. Kết quả kiểm thử (Summary Report)

| Label | Samples | Average (ms) | Min | Max | Std.Dev | Error % | Throughput |
|------|------|------|------|------|------|------|------|
| HTTP Request | 100 | 82 | 41 | 514 | 84.37 | 79% | 45.1/min |
| post | 100 | 171 | 135 | 393 | 27.81 | 0% | 16.4/min |
| trang chủ | 20 | 0 | 0 | 0 | 0 | 100% | 21.1/min |
| trang chủ | 50 | 74 | 42 | 201 | 45.86 | 82% | 39.1/sec |
| trang chủ | 50 | 55 | 42 | 86 | 7.77 | 62% | 1.7/sec |

### Tổng kết

- Total Requests: **320**
- Average Response Time: **99 ms**
- Max Response Time: **514 ms**
- Throughput trung bình: **36.5 requests/min**
- Error Rate: **53.44%**

---

## 5. Phân tích kết quả

- Thời gian phản hồi trung bình của hệ thống khoảng **99 ms**, cho thấy server phản hồi khá nhanh trong nhiều trường hợp.
- Request tới endpoint `/posts` có **0% lỗi**, chứng tỏ API này hoạt động ổn định.
- Một số request tới **trang chủ có tỷ lệ lỗi cao (62% – 100%)**, có thể do:
  - URL không đúng
  - Website chặn request từ công cụ test
  - Endpoint yêu cầu xác thực

---

## 6. Cấu trúc repository
bài tập kiểm thử jmeeter │
├── fileJmx.jmx
├── summary.csv
screenshots
└── README.md

---

## 7. Minh chứng

Repository bao gồm:

- File cấu hình JMeter (`.jmx`)
- File kết quả kiểm thử (`.csv`)
- Screenshot 
- File README báo cáo kết quả# B-i-t-p-ki-m-th-hi-u-n-ng-trang-web-JMeter-
