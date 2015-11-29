> Source: http://kipalog.com/posts/Toi-da-dung-Docker-nhu-the-nao

**Pull một image từ Docker Hub**

```docker pull <image name>```

**Tạo một container từ image có sẵn**

```docker run -v <thư mục trên máy tính>:<thư mục trong container> -it <image name> /bin/bash```

Lệnh trên tạo container, liên kết một thư mục trên máy tính vào bên trong container, và truy cập vào chế độ dòng lệnh của container đó.

Đối với các ứng dụng như web, container sẽ tạo một web server trên một cổng nào đó, khi đó chúng ta cần phải map cổng đó từ container ra máy tính ngoài, khi đó chúng ta dùng thêm tham số -p như sau:

```docker run -v /abc:/abc -p 80:80 -it ubuntu /bin/bash```

Lệnh trên map cổng 80 của container ra cổng 80 của máy tính hiện tại.

Ngoài ra, Còn một số lệnh khác mà các bạn có thể dùng để quản lý Docker của mình:

**Liệt kê các images hiện có**

```docker images```

Trong kết quả trả về của lệnh này, chúng ta lưu ý các thông số:

- *TAG:* là tên của image, ví dụ lukasz/docker-scala
- *IMAGE ID:* là ID của image lưu trong hệ thống, ví dụ 91e54dfb1179

**Liệt kê các container đang chạy**

```docker ps```

Trong kết quả của lệnh này cũng có các thông số chúng ta cần lưu ý, đó là:

- *CONTAINER ID:* Là ID của container đó, ví dụ 4cc671941ee3
- *NAME:* Là tên riêng của container, được tạo ra một cách ngẫu nhiên hoặc có thể tự đặt, ví dụ stupefied_blackwell

**Liệt kê toàn bộ các container đang chạy và đã tắt**

Sau khi các bạn thoát khỏi container, nếu nó không còn chạy bất cứ một tiến trình nào nữa, thì nó sẽ tự động tắt, nhưng chưa hoàn toàn bị xoá, khi đó chạy lệnh docker ps sẽ ko thấy được. Để xem lại nó thì chúng ta dùng lệnh sau.

```docker ps -a```

**Khởi động và truy cập lại vào một container đã tắt**

Nếu một container đã tắt (không xuất hiện khi dùng lệnh docker ps nữa, chúng ta có thể chạy lệnh ```docker ps -a``` để lấy ID hoặc NAME của nó, sau đó dùng lệnh sau để khởi động và truy cập lại vào đó)

```docker start <ID hoặc NAME>```
```docker exec -it <ID hoặc NAME> /bin/bash```

**Xoá một container**

Nếu một container đã hết giá trị lợi dụng, dù nó đã tắt nhưng nó vẫn chiếm một phần dung lượng trên máy tính, để xoá nó đi, chúng ta dùng lệnh rm

```docker rm <ID hoặc NAME>```

Nếu container đang chạy, bạn cũng có thể xoá nhưng phải thêm tham số -f vào sau rm để force remove:

```docker rm -f <ID hoặc NAME>```

**Xoá một image**

Cũng như container, nếu bạn đã ko còn nhu cầu sử dụng một image nào đó nữa, thì nên xoá nó đi, vì dung lượng nó khá là nặng, để lại chật máy. Dùng lệnh rmi (tức là remove image đó)

```docker rmi <ID hoặc NAME>```

hoặc

```docker rmi -f <ID hoặc NAME>```