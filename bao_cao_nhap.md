# BAO CAO THUC HANH HADOOP – PHAN TICH DOANH THU THEO NHOM SAN PHAM
Sinh vien: ......  MSSV: ......
Moi truong: Google Colab, Apache Hadoop 3.5.0, Java 17, Hadoop Streaming (Python). Che do local MapReduce; HDFS pseudo-distributed (NameNode + DataNode) tren cung may ao.

## 1. Du lieu dau vao
File orders_2026_09.csv gom 1,500 giao dich thang 09/2026, 11 truong (transaction_id, order_date, order_time, province, category, channel, quantity, unit_price, amount, status, shipping_days). Trong do 1,240 giao dich SUCCESS, 142 FAILED, 118 RETURNED. Chi giao dich SUCCESS duoc tinh doanh thu. Tren HDFS file nam o /user/student/ecommerce/input/.

## 2. Mapper
Mapper doc tung dong CSV tu standard input. Neu status = SUCCESS thi phat sinh cap key-value: category -> amount (vi du: Electronics -> mot gia tri amount). Cac giao dich FAILED/RETURNED bi bo qua.

## 3. Reducer
Sau buoc Shuffle/Sort, cac dong cung category duoc gom lai. Reducer cong tong amount cua tung category va ghi ket qua cuoi vao part-00000.

## 4. Ket qua Top 3
| Hang | Category | Doanh thu (VND) | Ty trong | Nhan xet |
|---|---|---|---|---|
| 1 | Electronics | 3,703,769,311 | 76.9% | (tu viet) |
| 2 | Home | 410,315,065 | 8.5% | (tu viet) |
| 3 | Fashion | 218,597,763 | 4.5% | (tu viet) |

Tong doanh thu SUCCESS: 4,814,079,444 VND.

## 5. Nhan xet kinh doanh (5-7 dong – TU VIET LAI BANG LOI CUA EM)
Goi y y tuong: Electronics dan dau (3,703,769,311 VND, chiem 76.9% tong doanh thu), gap 9.0 lan nhom thu hai (Home); nhom thu ba la Fashion. Phan tich: rui ro phu thuoc vao mot nhom, de xuat ton kho/khuyen mai/giao hang, luu y da loai FAILED va RETURNED.

## 6. Lien he HDFS – MapReduce – YARN
HDFS luu tru phan tan du lieu theo cay thu muc; MapReduce xu ly theo mo hinh key-value (Map -> Shuffle/Sort -> Reduce); YARN quan ly tai nguyen va lap lich cac task cua job.

## 7. Han che cua xu ly batch
(Viet 1-2 cau: ket qua chi co sau khi job chay xong, khong phu hop nhu cau thoi gian thuc, job co chi phi khoi dong...)
