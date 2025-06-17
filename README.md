# SMART_LIBRARY_FOR_HCMUTE_STUDENTS
My system includes: Computer Vision (Face Recognition), OCR, Natural Language Processing (RAG) and Reinforcement Learning (Deep Q-Learning)

# 📚 Hệ thống Thủ thư Thông minh Hỗ trợ Sinh viên - HCMUTE

> Khóa luận tốt nghiệp - Kỹ sư Công nghệ Thông tin  
> Sinh viên: Nguyễn Thi Phú (21110600), Bùi Quang Thiện (21110656)  
> Giảng viên hướng dẫn: ThS. Lê Minh Tân  
> Trường Đại học Sư phạm Kỹ thuật TP.HCM

---

## 📌 Mục tiêu

Xây dựng hệ thống thư viện thông minh giúp sinh viên:
- Đăng nhập bằng khuôn mặt (Face Recognition).
- Thêm sách qua ảnh bìa (OCR).
- Tư vấn sách qua chatbot AI.
- Gợi ý sách cá nhân hóa dựa trên lịch sử truy vấn.

---

## 🛠️ Công nghệ sử dụng

| Thành phần | Công nghệ |
|------------|-----------|
| Ngôn ngữ | Python, HTML/CSS/JS |
| Backend | Django, Flask |
| Frontend | Django Template |
| AI/NLP | LLaMA/Gemma (LLM), SentenceTransformer |
| OCR | PaddleOCR, VietOCR |
| Vector Search | ChromaDB |
| Cơ sở dữ liệu | SQL Server |
| Nhận diện khuôn mặt | MTCNN, InceptionResNetV1 |
| Reinforcement Learning | Deep Q-Learning |
| Truy vấn sách | Google Books API (mã ISBN) |

---

## 🧠 Thuật toán và kỹ thuật

### 1. Nhận diện khuôn mặt
- **MTCNN**: Phát hiện và căn chỉnh khuôn mặt.
- **InceptionResNetV1**: Trích xuất vector đặc trưng (512 chiều).
- **Cosine Similarity**: So sánh với vector đã lưu để xác thực.

### 2. Trích xuất thông tin sách
- **OCR**: PaddleOCR/VietOCR nhận dạng tiêu đề & tác giả từ ảnh bìa.
- **LLM**: Xác định chủ đề, phân loại nội dung tự động.

### 3. Chatbot hỏi đáp sách
- **RAG (Retrieval-Augmented Generation)**:
  - Truy vấn ChromaDB để lấy phần giới thiệu sách.
  - LLM sinh câu trả lời từ dữ liệu được truy xuất.

### 4. Gợi ý sách cá nhân hóa
- **Deep Q-Learning**:
  - Trạng thái: embedding câu hỏi, lịch sử truy vấn.
  - Hành động: đề xuất sách.
  - Phần thưởng: click, phản hồi người dùng.

---

## 🖥️ Yêu cầu phần cứng

| Thành phần | Yêu cầu |
|------------|--------|
| CPU | Intel Core i5 trở lên |
| RAM | Tối thiểu 8 GB |
| GPU | Khuyến nghị: NVIDIA GPU >= 4GB VRAM (nếu chạy LLM lớn) |
| Ổ cứng | SSD >= 10 GB trống |
| Hệ điều hành | Ubuntu 20.04+, Windows 10+ |

---

## 🗄️ Cơ sở dữ liệu

### SQL Server (CSDL chính)
- **User**: thông tin sinh viên/thủ thư.
- **Book**: thông tin sách.
- **BookIntro**: phần giới thiệu sách (văn bản).
- **Chat**: lịch sử hội thoại người dùng - chatbot.
- **UserBookInteraction**: theo dõi hành vi, phản hồi người dùng.

### ChromaDB (CSDL vector)
- Lưu vector embedding từ phần mở đầu sách.
- Hỗ trợ truy vấn ngữ nghĩa nhanh và hiệu quả.

---

## 🔁 Quy trình hệ thống

```mermaid
flowchart TD
    A[Người dùng] -->|Đăng nhập bằng khuôn mặt| B(MTCNN + InceptionResNetV1)
    B --> C{Đúng người dùng?}
    C -- Không --> X[Thông báo lỗi]
    C -- Có --> D[Truy cập hệ thống]

    D -->|Thêm sách bằng ảnh| E[PaddleOCR + LLM]
    E --> F[Trích xuất tiêu đề, tác giả]

    D -->|Thêm sách bằng ISBN| G[Truy xuất Google Books API]

    D -->|Tra cứu sách| H[Người dùng nhập câu hỏi]
    H --> I[Embedding câu hỏi]
    I --> J[Truy vấn ChromaDB]
    J --> K[LLM sinh câu trả lời]

    D -->|Xem gợi ý sách| L[Deep Q-Learning]
    L --> M[Đề xuất sách cá nhân hóa]
