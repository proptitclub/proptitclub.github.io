---
layout: project_single
title:  "TekoRecommendModel"
slug: "TekoRecommendModel"
user: tuenv2kProPTIT
repo : TekoRecommendModel
git: True
---


# update docs in future
---
#  Recommended

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


---

#  Bài Toán 

**Input là một trang web có user và các sản phẩm.**

**Output đưa ra các gợi ý hợp lí cho user trong hiển thị sản phẩm, filter rank search.**

---

# Dữ liệu

## User 

User gồm các thông tin cơ bản. Trong đó sử dụng 1 số thông tin quan trọng cho model như :

1. Id_user (unique)
1. Nơi ở hiện tại
1. Nghề Nghiệp (Sinh viên)

## Sản phẩm 

Sản phẩm bao gồm các thông tin cơ bản để extract feature:

1. Id_product
1. Giá Thành
1. Loại sản phẩm
1. Nơi sản phẩm có thể cung cấp

## Dữ liệu tracking

Mỗi một lượt clicks ta sẽ lưu lại thông tin sau để làm dữ liệu train model.

1. Tất cả thông tin user
1. Tất cả thông tin product
1. Thời gian xem sản phẩm user đó.
1. Thời lượng xem sản phẩm user đó 

**Ngoài ra còn có thể lưu rất nhiêu thuộc tính khác của user-product-tracking để extract feature cho model.**

# Model

Việc personalize tìm kiếm là khác phức tạp. Nó đòi hỏi rất nhiều yếu tố user-sản phẩm, sản phẩm - user , user- user, thời gian, địa điểm, ngoải ra ta còn có thể khai thác rất nhiều thông tin hữu ích... Nên việc tiếp cận theo hướng rating **[Matrix Factorization Collaborative Filtering](https://machinelearningcoban.com/2017/05/31/matrixfactorization/)** là không được khả quan.

**[DeepFM:](https://www.ijcai.org/Proceedings/2017/0239.pdf)** đã tận dụng mô hình MF và khả năng học hiệu quả của deeplearning cho ra kết quả tốt.

> Ảnh mô hình DEEPFM
![Imgur](https://i.imgur.com/i7pUEgW.png)

---

Mô hình gồm 2 stage: 

1. Factorization-Machine 
2. Mạng deeplearning đơn giản.

## Factorization-Machine 

Với **[Matrix Factorization Collaborative Filtering](https://machinelearningcoban.com/2017/05/31/matrixfactorization/)** chúng ta bị hạn chế bởi số lượng feature hạn chế (user-item).Ý tưởng **[d-way Factorization Machine](https://www.csie.ntu.edu.tw/~b97053/paper/Rendle2010FM.pdf)** là cho các feature tương tác với nhau để tim ra các thuộc tính ẩn, lúc này chúng ta có thể tự do chọn lựa các feature phù hợp bài toán của mình.

### Equation:
![Imgur](https://i.imgur.com/AOMCmA1.png)

## deeplearning

deeplearning sử dụng các model mlp đơn giản đê huấn luyện mô hình.

---

## PipeLine

1. Đầu vào là một vector $x^{1*d}$ d feature.

2. Đầu tiên ứng mỗi feature được đưa vào lớp embedding, có outshape là K ở đây K là hệ số sấp sỉ ma trận trong Matrix Factorization. Ta thu được một vector X có size = d*k.

    * X đi vào stage **Factorization-Machine** cho ra một số scalar.
    * X đi vào mạng deeplearning output ra một scalar.
3. tính tổng kết quả ở 2 stage cho ra kết quả. (Có thể cho qua các layer như softmax với bài toán classifier)

> **Sử dụng model deepMF để predict ra khả năng clicks vaò các sản phẩm của trang web. Việc này khá giống cách làm offline, mỗi user ta sẽ tính toán score clicks của tất cả sản phẩm hiện tại, sau đó gán score đó vào database để recommend top score.**

---

## Kinh nghiệm

### Weights

K trong [Matrix Factorization](https://machinelearningcoban.com/2017/06/07/svd/)

![](https://machinelearningcoban.com/assets/25_mf/mf1.png)

Mô hình deepMF nặng tới đâu tất cả phụ thuộc rất lớn vào hệ số K (factors). Việc tăng hệ số K giúp ta sấp sỉ mô hình tốt. 

Tuy nhiên trong thực tế số lượng user và sản phẩm là rất lớn còn chưa kể đến các feature mà chúng ta lựa chọn thêm.

Output của lớp embedding sẽ là tổng số lượng unique ở tất cả feature * K, vì thế nên chọn K nhỏ khoảng 10-15. 

**Khi K đủ lớn việc tăng thêm K là không cần thiết**. [xem thêm](https://machinelearningcoban.com/2017/06/07/svd/) 

---

## Ưu điểm 

1. Predict offline - Recommend online.
2. Mô hình nhỏ có thể dùng cpu để train.
3. Mô hình phù hợp với bài toán cần phải có nhiều feature để trích xuất thông tin.

---

## Hạn chế.

1. Khi có một sản phẩm,user mới hoặc feature xuất hiện thêm các tiền lệ chưa có thì cần trainning lại.
    * Do đặc tính embedding thì việc thêm 1 user vào sẽ thêm 1 vector trong embedding các vector khác không thay đổi.
    * Trainning lại thì có thể transfer được.

2. Chưa có đủ data để train model và đánh giá chính xác. Data cũng rất khó để dùng cơm fake :v.

---




