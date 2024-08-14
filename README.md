# AsakaStartup
 > **AsakaStartup** là một script khởi động Java được viết lại dựa trên [**Aikar's Flags**](https://docs.papermc.io/paper/aikars-flags) bởi [**Asaka Cloud**](https://asakacloud.vn), thiết kế để tối ưu hóa hiệu suất cho các máy chủ.
 
> **Các mục tiêu mà script này tập trung vào:**
- Script này tập trung vào việc tối đa hóa việc sử dụng CPU và giảm thiểu việc sử dụng RAM nhằm nâng cao hiệu quả tổng thể
- Script này phù hợp để sử dụng trên máy chủ Minecraft nhằm cải thiện hiệu suất. Bạn cũng có thể sử dụng các arguments ở dưới, áp dụng trên Minecraft Client (hoặc là các launcher khác như TLauncher / Legacy / Pojav, chỉ cho phiên bản 1.20 trở lên) để tăng FPS. Lưu ý rằng việc sử dụng script này trong thời gian dài có thể gây ra sự cố hoặc làm cho trò chơi bị treo.

## Cách để chạy
> **Linux: Dùng trực tiếp lệnh khởi động ở bên dưới**

> **Windows: [Tải file](https://raw.githubusercontent.com/asakacloud/AsakaStartup/main/run.bat) chạy server về máy và chạy trên máy của bạn ( Nhớ chỉnh số ram bạn muốn chạy ở phần -Xmx8192M**

> **Hosting ( Các dịch vụ host như là Asaka Cloud, DPT, MCViet, v.v ): Bạn có thể liên hệ với đội ngũ hỗ trợ của host để nhờ chỉnh startup script trên host của bạn**

## Câu Lệnh Khởi Động

>  ```java -Xms128M -Xmx(Max RAM Server của bạn)M -XX:MaxRAMPercentage=95 -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:+EnableDynamicAgentLoading -XX:+UnlockExperimentalVMOptions -XX:MaxGCPauseMillis=200 -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=15 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=10 -XX:G1MixedGCLiveThresholdPercent=85 -XX:G1RSetUpdatingPauseTimePercent=1 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -XX:MinHeapFreeRatio=10 -XX:MaxHeapFreeRatio=20 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -Dterminal.jline=false -Dterminal.ansi=true -jar server.jar nogui```

## Giải Thích Các Arguments trong đoạn script:
- **XX:MaxRAMPercentage=95**: Phân bổ tối đa 95% RAM của hệ thống cho JVM. Điều này giúp tận dụng gần như toàn bộ RAM có sẵn.
- **XX:+UseG1GC**: Kích hoạt garbage collector G1, thích hợp cho các ứng dụng có heap lớn và yêu cầu độ trễ thấp.
- **XX:+ParallelRefProcEnabled**: Kích hoạt xử lý song song các đối tượng tham chiếu, cải thiện hiệu suất garbage collection.
- **XX:+EnableDynamicAgentLoading**: Cho phép tải động các agent Java, hữu ích cho việc phát triển và kiểm tra.
- **XX:+UnlockExperimentalVMOptions**: Kích hoạt các tùy chọn VM thử nghiệm, cho phép sử dụng các tính năng mới chưa chính thức.
- **XX:MaxGCPauseMillis=200**: Đặt thời gian dừng tối đa cho garbage collection là 200 ms, giúp giảm độ trễ do GC.
- **XX:+DisableExplicitGC**: Vô hiệu hóa các cuộc gọi garbage collection explicit (các cuộc gọi GC do ứng dụng yêu cầu).
- **XX:+AlwaysPreTouch**: Đảm bảo rằng tất cả bộ nhớ được chạm trong quá trình khởi động JVM, giúp cải thiện hiệu suất.
- **XX:G1NewSizePercent=30**: Đặt tỷ lệ phần trăm kích thước heap được sử dụng cho không gian thế hệ mới là 30%.
- **XX:G1MaxNewSizePercent=40**: Đặt tỷ lệ phần trăm tối đa của kích thước heap được sử dụng cho không gian thế hệ mới là 40%.
- **XX:G1HeapRegionSize=8M**: Đặt kích thước mỗi vùng G1 là 8 MB. Điều này ảnh hưởng đến cách phân chia bộ nhớ của G1 GC.
- **XX:G1ReservePercent=15**: Đặt tỷ lệ phần trăm heap dự trữ cho garbage collector G1 là 15%, giúp đảm bảo có đủ bộ nhớ cho GC.
- **XX:G1HeapWastePercent=5**: Đặt tỷ lệ phần trăm chất thải heap được phép bởi G1 GC là 5%.
- **XX:G1MixedGCCountTarget=4**: Đặt số lượng garbage collection mixed mục tiêu trước khi thực hiện một garbage collection mixed.
- **XX:InitiatingHeapOccupancyPercent=10**: Đặt tỷ lệ phần trăm chiếm dụng heap mà G1 bắt đầu một garbage collection đồng thời khi đạt 10%.
- **XX:G1MixedGCLiveThresholdPercent=85**: Đặt tỷ lệ phần trăm dữ liệu sống cần được giữ trong một vùng để đủ điều kiện cho garbage collection mixed là 85%.
- **XX:G1RSetUpdatingPauseTimePercent=1**: Đặt tỷ lệ phần trăm thời gian dừng tối đa cho các cập nhật RSet là 1%.
- **XX:SurvivorRatio=32**: Đặt tỷ lệ không gian survivor so với không gian Eden là 32, ảnh hưởng đến cách phân bổ bộ nhớ trong các khu vực thế hệ trẻ.
- **XX:+PerfDisableSharedMem**: Vô hiệu hóa việc sử dụng bộ nhớ chia sẻ cho giám sát hiệu suất, giúp giảm overhead bộ nhớ.
- **XX:MaxTenuringThreshold=1**: Đặt số lần tối đa mà một đối tượng có thể được thăng cấp từ thế hệ trẻ sang thế hệ cũ trước khi bị thăng cấp là 1.
- **XX:MinHeapFreeRatio=10**: Đặt tỷ lệ phần trăm bộ nhớ heap miễn phí tối thiểu trước khi thu hẹp heap là 10%.
- **XX:MaxHeapFreeRatio=20**: Đặt tỷ lệ phần trăm bộ nhớ heap miễn phí tối đa trước khi mở rộng heap là 20%.
## Một vài lưu ý:
> Quyền lợi: Chúng tôi **có quyền từ chối chịu bất kì trách nhiệm** nếu có các lỗi liên quan đến server của bạn sau khi sử dụng đoạn script này. 

>Tuy nhiên, đoạn script này đã được viết bởi [**Asaka Cloud**](https://asakacloud.vn) và hiện tại đang được áp dụng cho các khách hàng sử dụng Hosting tại [**Asaka Cloud**](https://asakacloud.vn) và được tối ưu rất tốt, nên bạn có thể yên tâm chạy đoạn script này trên Host / VPS của bạn.

## Sửa lỗi và cập nhật:
> Sẽ được cập nhật và sửa đổi thêm trong [**Server Discord**](https://discord.gg/asakacloud) của chúng tôi.