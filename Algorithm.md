# Big-O
## Tại sao phải quan tâm tới độ phức tạp của thuật toán

Ví dụ như này:
```
Bạn được vợ yêu cầu đi mua 4 ổ bánh mì (cho vợ và 3 đứa con) mà bạn lại thì đang vội lên công ty. 
- Cách thứ nhất là: bạn mua ổ bánh mì có ớt cho vợ, mang về nhà đưa vợ (chờ quán làm tiếp mấy ổ khác), rồi quay lại mang ổ thứ 2 cho đứa con cả,... cứ thế. Mất 4 lượt đi lại.
- Cách thứ hai là: bạn chờ quán làm đủ 4 ổ bánh mì, buộc lại, đưa lên drone để điều khiển nó mang về nhà (hàng không thì không bị tắc), trong khi đó bạn vẫn đi lên công ty được.
```
Xem ở [phần]() để thấy thêm tác dụng của thuật toán tốt.

## Cẩn thận hiểu lầm Big-O

- ***Big-O*** sinh ra là để ***mô tả độ phức tạp*** của thuật toán chứ ***KHÔNG*** dùng để tính thời gian thực thi.


> Thời gian thực thi của chương trình còn phụ thuộc vào: data, resource, memory,...
> + data: vd size của biến
> + Space complexity: là độ phức tạp bộ nhớ.
> + resource: tài nguyên máy tính (siêu máy tính khác với máy tính cùi bắp)


## 12. Một số độ phức tạp thường gặp:
Tham chiếu từ [Ref.3]

### O(n): Độ phức tạp tuyến tính. 

Xét hàm tính tổng các số từ 1 đến n sau:

```
int sum(int n)
{
    int s = 0;
    for(int i = 1; i <= n; i++)
        s += i;
    return s;
}

```
- Với mỗi giá trị khác nhau của `n` thì số lần thực thi của vòng lặp trên là `n` lần. Chính vì vậy ***thời gian thực thi*** của chương trình trên phụ thuộc vào giá trị đầu vào `n`. 
- Func trên phải thực hiện `n+2` step ---> ***độ phức tạp*** của chương trình trên là  `O(n+2)` ---> rút gọn lại là `O(n)`.

> Step1: gán `s`
> Step2->n+1: tính s += i (n lần)
> Step(n+2): return.

**Cũng là cách tính tổng*** nhưng có độ phức tạp thuật toán là O(1)

```
int sum(int n)
{ 
    return n*(n+1)/2;
}

```
- Với *mọi* giá trị đầu vào chương trình chỉ thực thi đúng 1 câu lệnh return. 
- Độ phức tạp của chương trình trên là `O(1)`.

***Cùng*** là một bài toán, nhưng độ phức tạp của thuật toán là khác nhau (tức thời gian thực hiện khác nhau), vậy nên mới cần tới ***giải thuật*** và cần tới ***độ phức tạp*** .

### O(n²): 

O(n²): Thường gặp khi có 2 vòng lặp lồng nhau. 

Xét hàm sắp xếp đổi chỗ trực tiếp (interchange Sort) sau:

```
void interchangeSort(int *a, int n)
{
   for (int i = 0; i < n-1; i++)
      for (int j = i+1; j < n; j++)
         if (a[i] > a[j])
         {
            int temp = a[i];
            a[i] = a[j];
            a[j] = temp;
         }
}

```
- Trong hàm này, `i` sẽ chạy từ 0 đến (n - 2). 
- Ứng với mỗi giá trị của i, vòng `for` bên trong sẽ chạy `n - i - 1` lần (j từ `i + 1` đến `n - 1`)
- Số phép toán phải thực hiện là: `n²/2 - n/2` -->  ***độ phức tạp*** của thuật toán trên là  `O(n²/2 - n/2)` ---> rút gọn lại là `O(n²)`.


### O(logn): 

## Tính độ phức tạp thuật toán:
### Một số lưu ý để tính độ phức tạp thuật toán:

[N.1]. Khi xét big-O, ta luôn xét với n là 1 số vô cùng lớn, do đó có thế coi n là +∞.
[N.2]. Các bước thực thi không phụ thuộc vào giá trị đầu vào(ví dụ các phép tính toán, gán, so sánh,...) có độ phức tạp hằng số(O(1)).
[N.3]. Tổng các hằng số là 1 hằng số.
[N.4]. Tích của 1 số dương với +∞ cũng là +∞, tổng của 1 số với +∞ cũng là+∞.

### Quy tắc bỏ hằng số

Bỏ hằng số nghĩa là không cần biết bài toán của bạn là `O(93xN)` hay là `O(7749xN)` thì nó cũng là O(N).
- `x`: phép nhân (93xN: tức là 93 phép tính bị lặp lại N lần).
- ***Big-O*** sinh ra là để ***mô tả độ phức tạp*** của thuật toán chứ KHÔNG dùng để tính thời gian thực thi.

### Các bước để tính độ phức tạp thuật toán:

Gọi T là độ phức tạp thuật toán cần tìm:

- Step.1: Tính biểu thức T bằng cách cộng thời gian (số bước/số phép toán) thực thi của các câu lệnh trong thuật toán.
- Step.2: Xét số hạng có tốc độ tăng nhanh nhất khi n tiến đến +∞.
- Step.3: Lược bỏ các giá trị có thể lược bỏ được theo các quy tắc ở trên.
- Step.4: Giá trị của số hạng cuối cùng còn sót lại chính là độ phức tạp thuật toán cần tìm.

## Referral

[Ref.1] https://kipalog.com/posts/Bi-gau-bo-vi-khong-biet-Big-O-la-gi

[Ref.2] https://techmaster.vn/posts/34982/hieu-don-gian-ve-khai-niem-big-o-trong-lap-trinh

[Ref.3] https://codelearn.io/sharing/big-o-do-phuc-tap-cua-thuat-toan

[Ref.4] https://viblo.asia/p/big-o-giai-thich-boi-1-lap-trinh-vien-tu-hoc-PqORvNerRAB

[Ref.5] https://www.codelean.vn/2021/04/big-o-cach-tinh-o-phuc-tap-cua-thoi.html

[Ref.6] https://www.codelean.vn/2021/04/bai-tap-ve-cach-tinh-big-o-cho-code.html

[Ref.7] https://blog.vietnamlab.vn/bigo-notation/

[Ref.8] https://sites.google.com/site/quanghd/home/danh

[Ref.9] https://www.hapq.me/big-o/

[Ref.10] https://hocjavascript.net/cau-truc-du-lieu-va-giai-thuat/big-o-notation/

[Ref.11] https://howkteam.vn/course/cau-truc-du-lieu-va-giai-thuat/do-phuc-tap-thoi-gian-bigo-la-gi-4270
