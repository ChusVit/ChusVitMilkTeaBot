# 🦆 Casso Tea & Brew - AI Assistant (Telegram Bot)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![payOS](https://img.shields.io/badge/payOS-0052FF?style=for-the-badge&logoColor=white)
![Railway](https://img.shields.io/badge/Railway-131415?style=for-the-badge&logo=railway&logoColor=white)

Một hệ thống Chatbot AI tự động hóa toàn diện quy trình tư vấn, đặt món và thanh toán cho hệ thống quán **Casso Tea & Brew** trên nền tảng Telegram. Dự án được thiết kế dưới dạng MVP nhằm tối ưu hóa quy trình bán hàng, tự động đối soát tài chính và nâng cao trải nghiệm khách hàng thông qua giao tiếp bằng ngôn ngữ tự nhiên.

## ✨ Tính năng nổi bật (Key Features)

- **🧠 Xử lý ngôn ngữ tự nhiên & Xưng hô linh hoạt:** Tích hợp `gpt-4o-mini` với bộ nhớ hội thoại. Bot có khả năng bóc tách thực thể (Món, Size, Số lượng) từ ngôn ngữ tự nhiên và áp dụng "Ma trận xưng hô" bản địa (tự động điều chỉnh đại từ nhân xưng dựa trên cách khách hàng gọi).
- **🛠️ Tích hợp Tool Calling & Logic Thành viên:** Kết nối LLM với cơ sở dữ liệu thông qua cơ chế Function Calling. Hệ thống tự động kiểm tra khách hàng cũ/mới để áp dụng kịch bản giảm giá 10% và tích điểm.
- **🛡️ Bảo mật & Chống thao túng (Guardrails):** Hệ thống được thiết lập ranh giới vai trò nghiêm ngặt, tự động khước từ các yêu cầu ngoài luồng (như viết code, giải toán, bàn luận chính trị).
- **💳 Thanh toán bất đồng bộ (payOS Webhook):** Khởi tạo VietQR động trực tiếp trong chat. Webhook Server lắng nghe sự kiện, tự động gửi tin nhắn "Ting Ting" chốt đơn tức thời.

## 🏗️ Kiến trúc hệ thống (System Architecture)

Dự án áp dụng kiến trúc Microservices tinh gọn và xử lý sự kiện bất đồng bộ (Event-driven) để đảm bảo khả năng chịu tải cao, không xảy ra tình trạng nghẽn cổ chai (bottleneck).

- **Tầng Giao tiếp (Client Layer):** Telegram Bot API hoạt động như UI/UX chính, tương tác với khách hàng theo thời gian thực.
- **Tầng Ứng dụng (Application Layer):** - `aiogram 3.x`: Xử lý luồng hội thoại bất đồng bộ.
  - `FastAPI`: Đóng vai trò là Webhook Gateway độc lập, mở cổng lắng nghe tín hiệu thanh toán từ hệ thống ngân hàng (thông qua payOS) 24/7.
  - `OpenAI API`: Đóng vai trò là "Bộ não" xử lý ngôn ngữ và trích xuất dữ liệu JSON cấu trúc hóa.
- **Tầng Dữ liệu (Data Layer):** Hệ quản trị cơ sở dữ liệu quan hệ PostgreSQL, quản lý toàn vẹn dữ liệu đơn hàng (Orders) và thông tin thành viên (Users).
- **Tầng Triển khai (Deployment Layer):** Toàn bộ hệ thống Backend và Database được đóng gói và tự động triển khai (CI/CD) trên nền tảng Cloud Platform-as-a-Service **Railway**.

## 💎 Giá trị kinh doanh (Business Value)

Hệ thống không chỉ là một sản phẩm công nghệ mà còn giải quyết trực tiếp các "nỗi đau" (pain points) trong vận hành F&B:

1. **Giảm ma sát mua sắm (Zero-friction Shopping):** Khách hàng không cần tải thêm ứng dụng hay truy cập website. Thao tác chọn món và thanh toán diễn ra 100% trên nền tảng chat quen thuộc, giúp tăng tỉ lệ chuyển đổi (Conversion Rate).
2. **Tự động hóa đối soát tài chính 24/7:** Giải phóng nhân sự thu ngân khỏi việc phải liên tục kiểm tra app ngân hàng để xác nhận chuyển khoản. Hệ thống tự động ghi nhận và báo cáo chính xác đến từng giao dịch.
3. **Cá nhân hóa và Quản trị khách hàng (CRM):** Khác với các web order thông thường, Chatbot chủ động lưu trữ dữ liệu người dùng. Việc tự động nhận diện khách quen và tặng ưu đãi giúp tăng mạnh tỉ lệ giữ chân khách hàng (Retention Rate).
4. **Tối ưu hóa luồng vận hành (Operation Flow):** Đơn hàng sau khi thanh toán thành công được phân luồng tự động và định dạng chuẩn hóa đẩy thẳng xuống bộ phận Bếp, giảm thiểu tối đa rủi ro sai sót do truyền đạt thủ công.

## 🚀 Hướng dẫn thử nghiệm (Testing Guide)

### ⚠️ LƯU Ý QUAN TRỌNG CHO BAN GIÁM KHẢO
> Hệ thống Backend và Database hiện đang được deploy và vận hành ổn định trên nền tảng Cloud **Railway**. Webhook lắng nghe giao dịch luôn trong trạng thái sẵn sàng (Active) để đảm bảo thời gian phản hồi tin nhắn thanh toán chỉ từ 2-5 giây.

**🔗 Link trải nghiệm Bot:** [Điền link Telegram Bot của bạn vào đây, ví dụ: https://t.me/CassoChusVitBot]

### Kịch bản Khuyến nghị (Recommended Test Cases)

Để trải nghiệm toàn bộ sức mạnh của hệ thống, Ban giám khảo có thể thực hiện theo các bước sau:
1. **Kiểm tra NLP:** Nhắn một câu đặt món dài, viết tắt hoặc cố tình đổi ý. *(VD: "Cho anh 1 trà sữa ô long lớn, à thôi đổi thành size vừa đi, với 2 cafe brew").*
2. **Kiểm tra Guardrails:** Thử yêu cầu bot làm toán hoặc viết mã code. Bot sẽ từ chối một cách khéo léo.
3. **Kiểm tra Logic Khách hàng:** Khi bot hỏi thông tin liên lạc, hãy nhập một số điện thoại bất kỳ. Ở lần đặt đầu tiên, bạn là khách mới. Nếu đặt thêm lần nữa với cùng SĐT đó, hệ thống sẽ tự nhận diện bạn là khách quen và giảm giá 10%.
4. **Kiểm tra Thanh toán (Ting Ting):** Chọn phương thức thanh toán Online, quét mã VietQR bằng app ngân hàng (hoặc app test). Ngay khi tiền về, bot sẽ chủ động nhắn tin cảm ơn và chốt đơn trong vài giây.

---

## 💻 Hướng dẫn cài đặt cho Developer (Local Development)

1. Clone repository này về máy:
   ```bash
   git clone [https://github.com/ChusVit/Casso-ChusVit-Final.git](https://github.com/ChusVit/Casso-ChusVit-Final.git)
   cd Casso-ChusVit-Final
   ```

2. Cài đặt các thư viện phụ thuộc:
   ```bash
   pip install -r requirements.txt
   ```

3. Thiết lập biến môi trường:
Tạo file .env ở thư mục gốc và điền thông tin các API Key tương ứng:
```bash
BOT_TOKEN=your_telegram_bot_token
OPENAI_API_KEY=your_openai_api_key
DB_URL=your_postgresql_connection_string
PAYOS_CLIENT_ID=your_payos_client_id
PAYOS_API_KEY=your_payos_api_key
PAYOS_CHECKSUM_KEY=your_payos_checksum_key
```

4. Khởi động server (Bot & Webhook):
```bash
python main.py
```
(Lưu ý: Để Webhook hoạt động trên Localhost, cần sử dụng ngrok để expose port của FastAPI ra ngoài Internet).

##👨‍💻** Tác giả**
Huỳnh Xuân Quốc Việt
Đại học Bách Khoa TP.HCM (HCMUT) - Sinh viên năm 3 (Chương trình Liên thông), chuyên ngành Khoa học Máy tính
Định hướng: Artificial Intelligence Engineer
GitHub: https://github.com/ChusVit
