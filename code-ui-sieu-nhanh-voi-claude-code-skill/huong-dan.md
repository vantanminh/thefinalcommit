# Hướng dẫn: Xây dựng Giao diện Web Siêu Tốc với AI (Claude Code, Next.js, shadcn/ui)

Chào mừng các bạn đã quay trở lại với kênh! Trong video này, chúng ta sẽ khám phá một quy trình làm việc hoàn toàn mới, nơi AI sẽ là trợ lý lập trình chính của bạn. Chúng ta sẽ dùng **v0.dev** để lên ý tưởng, sau đó đưa "bản thiết kế" đó cho **Claude Code** để tự động viết code component React. Cuối cùng, chúng ta sẽ tích hợp vào dự án **Next.js** với **shadcn/ui** và deploy lên **Vercel**.

---

## 📜 Nội dung chính

1.  **Cài đặt & Khởi động Claude Code**: Thiết lập môi trường AI để viết code.
2.  **Khởi tạo dự án Next.js & shadcn/ui**: Xây dựng nền tảng cho ứng dụng.
3.  **Lên ý tưởng & Tinh chỉnh Prompt với v0.dev**: Sử dụng v0.dev như một "sân chơi" để tạo ra câu lệnh hoàn hảo.
4.  **Dùng Claude Code để tạo Component**: Ra lệnh cho AI viết code dựa trên prompt đã tinh chỉnh.
5.  **Kiểm tra và Hoàn thiện**: Rà soát code do AI tạo và cài đặt các component còn thiếu.
6.  **Deploy lên Vercel**: Đưa sản phẩm lên mạng.

---

## 🛠️ Yêu cầu chuẩn bị

-   **Node.js**: Phiên bản 18.18 trở lên.
-   **pnpm**: Trình quản lý gói (`npm install -g pnpm`).
-   **Tài khoản GitHub** & **Tài khoản Vercel**.
-   **Trình soạn thảo code** (ví dụ: VS Code).

---

## 🚀 Các bước thực hiện

### Bước 1: Cài đặt & Khởi động Claude Code

Claude Code sẽ là công cụ chính giúp chúng ta biến ý tưởng thành code.

-   **Kho mã nguồn Claude Code**: [https://github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

    ```bash
    npm install -g @anthropic-ai/claude-code

    pnpm add -g @anthropic-ai/claude-code
    ```
1.  **Khởi động Claude Code:**
    Mở terminal và chạy lệnh sau để bắt đầu:
    ```bash
    claude --dangerously-skip-permissions
    ```

2.  **Cài đặt Plugin:**
    Trong giao diện Claude Code, chạy các lệnh sau để cài đặt plugin cần thiết cho việc thiết kế frontend:
    *   Thêm Marketplace:
        ```bash
        /plugin marketplace add anthropics/claude-code
        ```
    *   Cài đặt Plugin:
        ```bash
        /plugin install frontend-design@claude-code-plugins
        ```

### Bước 2: Khởi tạo dự án Next.js & shadcn/ui

Chúng ta sẽ tạo một dự án Next.js trống và sau đó thêm thư viện component `shadcn/ui`.

1.  **Tạo ứng dụng Next.js:**
    ```bash
    pnpm create next-app@latest my-ai-app --typescript --tailwind --eslint
    ```
    *(Thay `my-ai-app` bằng tên dự án của bạn)*

2.  **Di chuyển vào thư mục dự án:**
    ```bash
    cd my-ai-app
    ```

3.  **Khởi tạo shadcn/ui:**
    Lệnh này sẽ cấu hình các file cần thiết (như `tailwind.config.js`, `globals.css`...) để dự án của bạn có thể sử dụng các component từ shadcn/ui.
    ```bash
    pnpm dlx shadcn@latest init
    ```
    *(Chọn các tùy chọn mặc định hoặc tùy chỉnh theo ý muốn khi được hỏi)*

### Bước 3: Lên ý tưởng & Tinh chỉnh Prompt với v0.dev

Ở bước này, chúng ta **không lấy code** từ v0.dev. Thay vào đó, chúng ta dùng nó như một công cụ để xây dựng một câu lệnh (prompt) mô tả component thật chi tiết và hiệu quả.

1.  Truy cập [https://v0.dev](https://v0.dev).
2.  Bắt đầu với một ý tưởng đơn giản, ví dụ: *"A login form with email and password fields"*.
3.  Xem kết quả AI tạo ra. Sau đó, sử dụng tính năng "Iterate" (trò chuyện) để thêm các yêu cầu chi tiết hơn:
    *   *"Add a 'Forgot Password?' link."*
    *   *"Include social login buttons for Google and GitHub below the main button."*
    *   *"Make the main button purple."*
4.  Sau nhiều lần tinh chỉnh, bạn sẽ có một đoạn mô tả rất chi tiết. **Hãy sao chép đoạn mô tả cuối cùng này**, đây chính là "bản thiết kế" chúng ta sẽ đưa cho Claude Code.

### Bước 4: Dùng Claude Code để tạo Component

Bây giờ, hãy ra lệnh cho Claude Code viết code dựa trên prompt hoàn hảo mà bạn vừa tạo.

1.  Quay lại terminal đang chạy Claude Code.
2.  Yêu cầu Claude Code tạo một component mới. Ví dụ, để tạo component `LoginPage` trong file `src/app/page.tsx`, bạn có thể dùng lệnh:

    ```bash
    /edit src/app/page.tsx
    ```
    Sau đó, dán nội dung yêu cầu vào:
    
    > Create a new React component named 'LoginPage'. Use Tailwind CSS for styling and import necessary components like Button, Input, Card from '~/components/ui/...'. Here is the detailed description: [Dán prompt đã tinh chỉnh từ v0.dev vào đây]

3.  Claude Code sẽ phân tích yêu cầu và tự động viết code cho component đó.

### Bước 5: Kiểm tra và Hoàn thiện

Code do AI tạo ra có thể sử dụng các component của `shadcn/ui` mà chúng ta chưa cài đặt.

1.  **Xem lại code** mà Claude Code đã tạo.
2.  **Xác định các component** được sử dụng (ví dụ: `Button`, `Card`, `Input`, `Label`).
3.  Mở một terminal khác tại thư mục dự án và **cài đặt các component còn thiếu** đó:
    ```bash
    pnpm dlx shadcn-ui@latest add button card input label
    ```
    *(Thay thế danh sách component bằng những gì bạn thực sự cần)*.
4.  Chạy server dev (`pnpm dev`) để kiểm tra giao diện và đảm bảo mọi thứ hoạt động đúng.

### Bước 6: Deploy sản phẩm lên Vercel

Khi đã hài lòng với sản phẩm, hãy chia sẻ nó với mọi người.

-   **Trang chủ Vercel**: [https://vercel.app/](https://vercel.app/)

1.  Đẩy mã nguồn của bạn lên một repository trên GitHub.
2.  Đăng nhập vào Vercel, chọn **Add New...** > **Project**.
3.  Import repository GitHub của bạn.
4.  Vercel sẽ tự động nhận diện đây là dự án Next.js. Nhấn **Deploy** và chờ trong vài phút.
5.  Bạn sẽ nhận được một đường link công khai cho trang web của mình!

---

## 🔗 Tài nguyên & Liên kết

-   **Claude Code GitHub**: [https://github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)
-   **Hướng dẫn cài đặt shadcn/ui**: [https://ui.shadcn.com/docs/installation/next](https://ui.shadcn.com/docs/installation/next)
-   **Công cụ tinh chỉnh Prompt**: [https://v0.dev](https://v0.dev)
-   **Nền tảng Deploy**: [https://vercel.app/](https://vercel.app/)

---

Cảm ơn bạn đã theo dõi video! Nếu bạn thấy quy trình làm việc này thú vị, đừng quên nhấn **Like**, **Subscribe** và để lại bình luận nhé!
