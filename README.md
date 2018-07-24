# How-to-install-Windows-10-professional-Core-on-Raspberry-Pi-3-
CÀI ĐẶT WINDOWS 10 TRÊN RASPBERRY PI 3 
I. CHUẨN BỊ - Đầy đủ bộ Raspberry Pi 3;
- Thẻ nhớ 32Gb;
- Chuột, bàn phím, màn hình.
II. ĐỊNH DẠNG THẺ NHỚ 
1. https://www.partitionwizard.com/free-partition-manager.html (hoặc dùng Hirens.BootCD.15.2) 
2. Mở MiniTool. 
3. Cắm thẻ SD vào máy tính của bạn. 
4. Định dạng thẻ SD của bạn trong. Lưu ý: Thao tác này sẽ xóa tất cả dữ liệu. 
5. Tạo một phân vùng lớn hơn 100Mb và đặt tên là BOOT. 
6. Chọn định dạng FAT32. 
7. Nhấp vào OK. 
8. Tạo một phân vùng với bộ nhớ còn lại trên thẻ SD và đặt tên là Windows. 
9. Chọn định dạng là NTFS. 
10. Nhấp vào OK. 
11. Nhấp vào Áp dụng. 
12. Truy cập https://uup.rg-adguard.net/
  - Tải về các phiên bản có [arm64]
  - Chọn ngôn ngữ;
  - Chọn Windows 10 Professional;
  - Chọn Download ISO compiler trong OneClick! (unZIP -> RUN createISO.cmd) và tải xuống tệp.
13. Giải nén tập tin WoRP (link phía dưới video) sau đó copy vào ổ C 
14 Vào thư mục C:\WoRP\UEFI. 
15. Sao chép tất cả các tập tin trong thư mục UEFI và dán nó vào ổ BOOT của thẻ SD. 
16. Giải nén tệp creatingISO_17713.1000_en-us_arm64_Professional mà bạn đã tải xuống và đổi tên uup.  
17. Chạy createISO.cmd ISO sẽ được tạo ra, tuy nhiên, nó có thể mất một thời gian dài. 
(phần này tùy vào tình trạng internet của bạn) (mất khoảng 1h30p. để bạn có thể tạo thành được file .ISO) 
18. Trong thư mục C:\WoRP, tạo thư mục có tên "m". 
19. Nhấp chuột phải vào ISO, Open With, Windows Explorer. 
20. Sao chép install.wim vào thư mục C:\WoRP. 
21. Loại bỏ ISO bằng cách nhấp chuột phải vào nó và chọn Đẩy ra. 
22. Mở CMD với quyền admin. 
23. Chạy các lệnh trong tệp Commands 
Với E là Windows; D là ổ BOOT; 
Chạy lệnh 
  cd C:\WoRP 
  dism /Mount-image /imagefile:install.wim /Index:1 /MountDir:m
  dism /image:m /add-driver /driver:system32 /recurse /forceunsigned
  dism /unmount-wim /mountdir:m /commit
  dism /apply-image /imagefile:install.wim /index:1 /applydir:E:\
  bcdboot E:\Windows /s D: /f UEFI
  bcdedit /store D:\EFI\Microsoft\Boot\bcd /set {default} testsigning on
  bcdedit /store D:\EFI\Microsoft\Boot\bcd /set {default} nointegritychecks on
24. Đẩy thẻ SD ra. 
25. Lắp thẻ SD vào Raspberry Pi của bạn.
26. Bật Raspberry Pi 3. Có thể mất vài phút (hoặc lâu hơn) để khởi động. 
27. Sau đó cài đặt Windows như bình thường. Mất khoảng 15 phút cho khởi động vào màn hình chính..
