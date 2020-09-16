---
layout: post
title:  "Hướng dẫn viêt bài"
categories: [tutorial]
image: tutorial.1.jpeg
---

# Bố cục blog

Gồm 4 mục chính

1. _posts : Lưu tất cả các bài blog.
2. category.
3. project : lưu tất cả các bài trong team dự án, **Có thể viết trong _post cũng được nhưng 
sẽ không được liệt kê trong project.**
4. data : Gồm thông tin liên quan project.

---

# _post

Post được đặt vào bất kì folder nào trong _post đều được thậm chí là không nằm trong folder nào.Nguyên tắc là jeykyl sẽ lấy hết các post trong _post ra và chỉ phân loại theo tên.Ví dụ muốn làm 1 post về computer vison thì có thể taọ thêm folder computer vision trong _post, đê đẩy các bài vào cho dễ quản lí.

Nguyên tắc đặt tên post : **date:%Y-%m-%d-slug.md**

Nguyên tắc thêm Liquid vào 1 post : 1 post có thể có vô số tag tùy mục đích muốn sử dụng. Nhưng phải có đủ 3 tag sau:

1. layout: post 
2. title:  "Hướng dẫn viêt bài"
3. categories: [các category sẽ liệt kê vào đây]

Optional:
1. image : Lưu ảnh đại diện post.
2. github: True nếu muốn add link github vào cuối - cái này sẽ lấy API từ github để theo dõi số lượng start... trên 1 repo.

---

# Category

Mỗi một post sẽ có 1 category và nếu muốn post đó có thể xuất hiện theo category thì phải đảm bảo thư mục category có slug đó. Xem các category có sẵn để tùy chỉnh thêm category.

---
# Project-data

Project hoạt động tương tự như _post tuy nhiên để tách riêng post và các team dự án :v. Cái này như là 1 cách lọc sẵn category do em đặt ra thôi, mọi người hoàn toàn có thể viết trong post và đặt category là team dự án :v. Nhưng project thường có nhiều thứ quan tâm nên em nghĩ tách ra.

Do project gồm các post không trong _post của jeykyll nên phải viết 1 file config để dễ dàng sử dụng. (Các post không nằm trong _post sẽ không được đưa vào site.post).