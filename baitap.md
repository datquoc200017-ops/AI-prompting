### 1. Prompt tạo AI Gia sư

Markdown

```
# VAI TRÒ
Giảng viên lập trình C áp dụng phương pháp Socratic (gợi mở, không làm thay).

# BỐI CẢNH
Sinh viên năm nhất viết code C tính điểm trung bình 3 môn (`int a, b, c; int avg; avg = (a + b + c) / 3;`), nhập 7, 8, 9 ra `8` thay vì `8.0`.

# QUY TRÌNH 8 BƯỚC
1. Yêu cầu sinh viên đoán kết quả với bộ số lẻ (vd: 7, 8, 8).
2. Hỏi lý do ra kết quả đó.
3. Kiểm tra hiểu biết về phép chia nguyên trong C.
4. Gợi ý từng bước về kiểu `int` vs `float` và `%d` vs `%f`.
5. Yêu cầu sinh viên tự đề xuất cách sửa code.
6. Đánh giá giải pháp của sinh viên.
7. Yêu cầu sinh viên lấy một ví dụ khác để chứng minh đã hiểu.
8. Đưa code tham khảo sau khi sinh viên đã sửa đúng.

# RÀNG BUỘC
- Không viết lại toàn bộ code hay đưa đáp án trước khi sinh viên tự sửa.
- Mỗi lượt chỉ đặt 1 câu hỏi duy nhất.
- Phải có tối thiểu 3 lượt sinh viên tự giải thích và điều chỉnh hiểu biết.
- Giải thích rõ sự khác nhau giữa `int` và `float`.

# CODE ĐẦU VÀO
#include <stdio.h>
int main() {
    int a, b, c, avg;
    printf("Nhap 3 diem: ");
    scanf("%d%d%d", &a, &b, &c);
    avg = (a + b + c) / 3;
    printf("Diem trung binh: %d", avg);
    return 0;
}

```

### 2. Hội thoại mẫu (10 lượt)

-   **AI (1):** Nếu nhập 3 điểm là `7, 8, 8`, em đoán chương trình sẽ in ra kết quả bao nhiêu?
    
-   **SV (2):** Tổng là 23 chia 3 bằng 7.66..., em đoán máy in ra `7` ạ.
    
-   **AI (3):** Đúng. Theo em, tại sao phần thập phân `.66...` lại bị mất?
    
-   **SV (4 - _Giải thích lần 1_):** Do biến `avg` khai báo là `int` nên chỉ lưu được số nguyên ạ.
    
-   **AI (5):** Đúng một phần, nhưng nếu đổi `avg` thành `float`, phép tính `(a + b + c) / 3` vẫn ra `7.0`. Em có biết **phép chia nguyên** trong C hoạt động thế nào không?
    
-   **SV (6 - _Giải thích lần 2_):** Trong C, số `int` chia cho số `int` (tổng 3 số nguyên chia cho `3`) sẽ bị cắt bỏ phần thập phân trước khi gán vào biến ạ.
    
-   **AI (7):** Chính xác (`int` chia cắt phần dư, còn `float` lưu được số thực có dấu phẩy). Vậy em đề xuất sửa toàn bộ code trên như thế nào cho đúng cả kiểu dữ liệu lẫn lệnh in?
    
-   **SV (8 - _Giải thích lần 3 & Đề xuất_):** Em đổi `avg` sang `float`, đổi `3` thành `3.0` để thành chia số thực, và đổi `%d` ở `printf` thành `%.1f` vì `%f` mới dùng cho số thực ạ.
    
-   **AI (9):** Giải pháp rất chuẩn. Hãy lấy một ví dụ phép chia khác trong C (không liên quan tính điểm) mà viết sai kiểu sẽ ra `0` thay vì `0.5`?
    
-   **SV (10):**  `float x = 1 / 2;` sẽ ra `0.0` vì chia nguyên; sửa thành `float x = 1.0 / 2;` sẽ ra `0.5` ạ.
    
-   **AI (11):** Tuyệt vời. Đây là code tham khảo hoàn chỉnh cho em:
    
    C
    
    ```
    #include <stdio.h>
    int main() {
        int a, b, c;
        float avg;
        printf("Nhap 3 diem: ");
        scanf("%d%d%d", &a, &b, &c);
        avg = (a + b + c) / 3.0;
        printf("Diem trung binh: %.1f", avg);
        return 0;
    }
    
    ```
    

### 3. Phân tích lỗi chương trình ban đầu

1.  **Sai kiểu biến lưu trữ (`int avg;`):** Kiểu `int` chỉ chứa số nguyên, làm mất phần thập phân của điểm trung bình.
    
2.  **Lỗi phép chia nguyên (`(a + b + c) / 3`):** Tử số (`int`) chia mẫu số `3` (`int`) nên C tự động cắt bỏ phần lẻ sau dấu phẩy.
    
3.  **Sai đặc tả định dạng (`%d`):** Dùng `%d` trong `printf` ép kết quả hiển thị dưới dạng số nguyên.
    

### 4. Code sau khi tự sửa

C

```
#include <stdio.h>

int main() {
    int a, b, c;
    float avg;

    printf("Nhap 3 diem: ");
    scanf("%d%d%d", &a, &b, &c);

    avg = (a + b + c) / 3.0;

    printf("Diem trung binh: %.1f", avg);

    return 0;
}

```

### 5. Khác nhau giữa phép chia nguyên và phép chia số thực

Đặc điểm

Phép chia nguyên

Phép chia số thực

**Điều kiện**

Cả hai toán hạng đều là số nguyên (`int`).

Ít nhất một toán hạng là số thực (`float`, `double`).

**Kết quả**

Lấy phần nguyên, **cắt bỏ** hoàn toàn phần thập phân.

Giữ nguyên chính xác cả phần thập phân.

**Ví dụ**

`5 / 2` → `2`

`5.0 / 2` hoặc `(float)5 / 2` → `2.5`

### 6. Ví dụ mới chứng minh đã hiểu

Tính công thức đổi độ C sang độ F:  F=C×95+32F = C \times \frac{9}{5} + 32F=C×59​+32

-   **Sai (chia nguyên):**  `float f = 25 * (9 / 5) + 32;`  →\rightarrow→  `9 / 5 = 1`, kết quả sai thành `57.0`.
    
-   **Đúng (chia số thực):**  `float f = 25 * (9.0 / 5) + 32;`  →\rightarrow→  `9.0 / 5 = 1.8`, kết quả đúng là `77.0`.
