# Lab04-IO

Lab 04 được demo trên micro-controller TIVA LaunchPad TM4C123G
![IMG_7908](https://user-images.githubusercontent.com/40592382/55240329-4559c480-526b-11e9-826a-ccc94b657d04.jpg)
## Mô tả

Hệ thống gồm hai switch tích cực mức thấp SW1, SW2 có vai trò input (nối với các chân PF4 và PF0) và ba output (PF3,PF2,PF1) được nối đến một LED nhiều màu.

<img width="966" alt="Screen Shot 2019-03-29 at 16 40 31" src="https://user-images.githubusercontent.com/40592382/55223729-702f2300-5241-11e9-9c38-2ddf0abf5003.png">

Các tasks được thực hiện trong Lab này:
1. Sử dụng datasheet để check địa chỉ của các thanh ghi và gán chúng với tên có nghĩa. Ví dụ, xét GPIO DIRECTION của Port F. Base address của GPIO Port F là 0x40025000, địa chỉ offset của GPIO DIRECTION là 0x400. Vậy, gán địa chỉ 0x40025400 cho biến toàn cục GPIO_PORTF_DIR_R và sử dụng nó để truy cập đến GPIO DIR của PORT F.
```
#define GPIO_PORTF_DIR_R        (*((volatile unsigned long *)0x40025400))
```
2. Khởi tạo Port: bao gồm các bước
   - Kích hoạt clock cho Port
   - Tắt analog function trong thanh ghi GPIO_AMSEL
   - Clear bits trong thanh ghi PCTL
   - Set input/output
   - Clear bits trong thanh ghi Alternate function (GPIO_AFSEL)
   - Bật digital port trong thanh ghi GPIO_DEN

3. Bit masking: dùng toán tử logic AND và OR để set/clear các bit cần thiết, giữ nguyên trạng thái của các bit còn lại. Ví dụ, Port F là một output, mình muốn set bit 5 và clear bit 3.
```
GPIO_PORTF_DATA_R = (GPIO_PORTF_DATA_R&(~0x08))|0x20;
```
## Video demo
Phần demo ngắn có thể được tìm tại [đây](https://youtu.be/pbEmlJ3v3QY) được hỗ trợ bởi khoá học MOOC Embedded Systems - Shape The World: Microcontroller Input/Output của giáo sư Jonathan Valvano của Đại học Texas tại Austin.
