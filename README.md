# What is Docker

> "Docker allows you to package an application with all of its dependencies into a standardized unit for software development."

**Translate:** Docker cho phép bạn đóng gói app và tất cả dependencies của nó thành một đơn vị tiêu chuẩn hóa cho phát triển phần mềm.

**Dể hiểu hơn:** Docker cho phép bạn đóng gói app và tất cả dependencies của nó thành một container, cách ly khỏi môi trường dev của bạn, không ảnh hưởng tới môi trường của máy.

**VD:** Bạn code Rails, một ngày nào đó bạn muốn thử run 1 cái app Scala, bạn k muốn cài một đống tools, apps để run được nó, mắc công ảnh hướng tới environment hiện tại của máy. Giải pháp là lên Docker Hub kiếm 1 file scala image (tại thời điểm này thì tạm coi nó như 1 file máy ảo đê, cho dễ hiểu, lát sau mình sẽ phân biệt rõ hơn), sau đó bằng một cách thần kì nào đó quăng cái app scala đó vào cái file scala image đó, bùm, app đã chạy được :rocket:.


## Some Docker's benefits

- Docker images sẽ giúp các dev trong team có đc một môi trường dev đồng nhất, không mất công set up tùm lum stuff (nếu sài images của người ta :3).
- Lightweight (nhẹ): Các containers share cùng một OS (Linux kernel) nhờ Docker Engine -> chạy nhanh, hiệu suất cao, sử dụng tài nguyên máy hiệu quả hơn, nhất là RAM (đứng ở khía cạnh một người từng dùng VMWare tôi thích điều này =)))
- Open: Các containers có thể chạy trên cả các Microsoft OS chứ k chỉ các Linux distributions. Ảo vậy :v
- Secure: Containers cô lập apps và còn tạo ra 1 lớp bảo vệ cho app đó nữa. (k hiểu lắm -_-)

# How is this different from virtual machines?**

> Containers have similar resource isolation and allocation benefits as virtual machines but a different architectural approach allows them to be much more portable and efficient.

![][/img/what-is-docker-diagram.png]

![][/img/what-is-vm-diagram.png]

**VMS: ** Mỗi VM bao gồm app, các thư viện cần thiết để run app đó, và cả một OS -> nặng cả chục GB :v
**Containers: ** Chỉ gồm app và các denpendencies thôi, chúng nó share OS với containers khác. Chúng nó chạy độc lập với các containers khác và không phụ thuộc vào bất cứ infrastructure nào. Bất kì máy tính, bất kì nền tảng, thậm chí là trên mây cũng chạy được.

# How does this help you build better software?

> When your app is in Docker containers, you don’t have to worry about setting up and maintaining different environments or different tooling for each language. Focus on creating new features, fixing issues and shipping software.

Như đã nói ở VD trên, bạn chỉ code thôi, mọi chuyện setup, maintain, deploy hãy để containers lo :v. Nhưng để nó tự lo được thì bạn cũng phải tốn nhiều công sức đấy :3.

Một số benefits khác:

- Accelerate Developer Onboarding: Tăng tốc quá trình, giúp dev bắt tay vào code nhanh hơn.
- Empower Developer Creativity: Nôm na là giúp dev có thể thoải mái test languages, tools, thử mọi thứ mà không phải sợ hư máy, sợ conficts, issues, mất công fix :v
- Eliminate Environment Inconsistencies: Nhờ tính đóng gói app mà containers sẽ chạy trên bất kì nền tảng, chạy như chính nó chạy trên cái máy đã thiết kế ra nó, không lo ngại sự không nhất quán giữa các environment (trên các máy khác, trong test hay production,...).
- Easily Share and Collaborate on Applications: Thông qua việc chia sẽ các Docker images mà các devs có thể dễ dàng chia sẽ và đóng góp vào apps nhanh hơn, dễ dàng hơn. 
- Ship More Software Faster: Đẩy nhanh quá trình phát triển phần mềm