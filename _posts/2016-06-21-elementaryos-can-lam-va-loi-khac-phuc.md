---
layout: post
title: ElementaryOS những việc cần làm sau cài đặt và lỗi cần khắc phục
category: 
tags: linux
---
Ở bài viết này tôi không hướng dẫn cách cài đặt vì đã có khá nhiều hướng dẫn loại này, bạn chỉ cần Google chút là ra, do ElementaryOS dùng lõi Ubuntu nên sự khác biệt trong quá trình cài đặt không khác nhau nhiều. Sau đây là một vài vấn đề sau cài đặt mà tôi đã gặp phải và cách khắc phục sau một chút tìm hiểu muốn chia sẻ lại.

ElementaryOS chỉ chiếm khoảng 5GB dung lượng ổ cứng sau khi cài đặt, nhẹ một cách bất ngờ, nhưng bạn cũng cần Custom lại chút đỉnh cho phù hợp cũng như cài đặt thêm các phần mềm cơ bản cần thiết.

- Hiện có một hướng dẫn rất đầy đủ bằng tiếng Anh tại github: [How to Install the perfect Elementary OS?](https://gist.github.com/memoryleakx/7567474)
- [Lỗi Crash Network sau khi cài đặt cập nhật làm mất kết nối Internet](http://askubuntu.com/questions/727127/last-upgrade-crashes-network-manager-no-internet-connection-no-applet) (lỗi chung của Ubuntu 14.04)
  1. Bạn cần một cái máy tính khác để tải các thành phần cần thiết hoặc dùng đĩa LiveCD/ USB cài đặt: amd64 (64bit): [libnl](http://archive.ubuntu.com/ubuntu/pool/main/libn/libnl3/libnl-3-200_3.2.21-1_amd64.deb) [libnl-genl](http://archive.ubuntu.com/ubuntu/pool/main/libn/libnl3/libnl-genl-3-200_3.2.21-1_amd64.deb) [libnl-route](http://archive.ubuntu.com/ubuntu/pool/main/libn/libnl3/libnl-route-3-200_3.2.21-1_amd64.deb) i386 (32bit): [libnl](http://archive.ubuntu.com/ubuntu/pool/main/libn/libnl3/libnl-3-200_3.2.21-1_i386.deb) [libnl-genl](http://archive.ubuntu.com/ubuntu/pool/main/libn/libnl3/libnl-genl-3-200_3.2.21-1_i386.deb) [libnl-route](http://archive.ubuntu.com/ubuntu/pool/main/libn/libnl3/libnl-route-3-200_3.2.21-1_i386.deb)
  2. Trở lại hệ thống của bạn, copy 3 file .deb vào cùng một thư mục và chạy dòng lệnh để cài đặt: `sudo dpkg -i libnl-*.deb`
  3. Khởi động lại Network Manager: `sudo service network-manager restart`
- [Cài đặt ibus-unikey](http://elementaryos.stackexchange.com/questions/1431/how-do-i-install-ibus-on-freya), hiện Elementary OS chưa hỗ trợ đầy đủ vì chưa hiển thị được icon của Ibus trên thanh menu. Nhưng bù lại khi chuyển đổi bộ gõ qua lại hệ thống sẽ hiển thị một popup nhỏ để chúng ta nhận biết.
  1. Cài đặt Ibus-Unikey bằng cách vào Ubuntu Software Center search: Vietnamese Input Method để cài đặt. Hoặc chạy dòng lệnh: `sudo apt-get install ibus-unikey`
  2. Do chưa hỗ trợ đầy đủ nên sau khi cài đặt xong bạn phải dùng cửa sổ dòng lệnh để gọi giao diện cài đặt ibus ra: `ibus-setup` và chọn tab Input Method.
  3. Check vào “Customize Active Input Methods” sau đó thêm Unikey ở ô bên dưới. Đóng hộp thoại lại là có thể sử dụng. Chuyển đổi gõ tiếng Anh và tiếng Việt bằng cách ấn Ctrl + Space
  4. Nếu không được bạn cần chạy thêm dòng lệnh: `ibus-daemon -drx`
  5. Để ibus tự động chạy mỗi khi khởi động máy bạn cần vào Settings>Application>Startup và thêm `ibus-daemon -drx` là custom command.
- Lỗi không điều chỉnh được độ sáng màn hình khi dùng VGA Intel onboard (lỗi này cũng từ Ubuntu mà ra)
  1. Mở terminal tạo file config bằng dòng lệnh: `sudo touch /usr/share/X11/xorg.conf.d/20-intel.conf`
  2. Sử dụng một text editor bất kỳ hoặc phổ biến nhất là gedit: `sudo gedit /usr/share/X11/xorg.conf.d/20-intel.conf`
  3. Chèn đoạn code sau đây vào file:
```Section "Device"
        Identifier  "card0"
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
        BusID      "PCI:0:2:0"
EndSection```
. Tham khảo thêm: [Fix Brightness Control Not Working for Ubuntu 14.04 & Linux Mint 17](https://itsfoss.com/fix-brightness-ubuntu-1310/)
  4. Log out (đăng xuất) và Log In trở lại là xong.

Cơ bản là xong, bạn đã có thể làm việc với Linux một cách hiệu quả và khá đầy đủ. Với tốc độ phát triển của nguồn mở trên máy tính cá nhân hiện nay thì khá là chậm và khó mà bắt kịp được vói MacOS và Windows. Linux vẫn nằm ở vị trí vốn có của nó đó là dành cho những người thích tìm tòi vọc vạch, hay Dev.
