1. Mục tiêu

Chương trình quản lý hàng đợi xe tại trạm sạc VinFast.

Các lỗi cần khắc phục:

Sử dụng pop() khiến lấy xe cuối hàng đợi thay vì xe đầu tiên.
Sử dụng push() để thêm xe mới vào cuối hàng đợi.
Sửa điều kiện vòng lặp từ i <= length thành i < length để không truy cập phần tử ngoài phạm vi mảng.
2. Phân tích lỗi
Lỗi 1: Sử dụng pop() thay vì shift()

Mã nguồn ban đầu:

const xeVaoSac = hangDoiXeCho.pop();

pop() lấy phần tử cuối cùng của mảng.

Với dữ liệu:

const hangDoiXeCho = [
    '30A-98765',
    '29B-12345',
    '51C-45678'
];

pop() lấy:

51C-45678

Điều này không đúng với quy tắc FIFO vì xe 30A-98765 đến trước phải được vào sạc trước.

Cách sửa

Sử dụng:

const xeVaoSac = hangDoiXeCho.shift();

shift() lấy phần tử đầu tiên của mảng.

Kết quả đúng:

Xe vào sạc: 30A-98765
3. Sử dụng push() để thêm xe mới

Sau khi lấy xe đầu hàng đợi, xe mới được thêm vào cuối:

hangDoiXeCho.push('43D-88888');

Kết quả:

29B-12345
51C-45678
43D-88888

Đây là thao tác đúng vì xe mới đến được xếp sau các xe đang chờ.

4. Lỗi vòng lặp

Mã nguồn ban đầu:

for (let i = 0; i <= hangDoiXeCho.length; i++) {
    console.log(STT ${i + 1}: ${hangDoiXeCho[i]});
}

Nếu mảng có length = 3 thì index hợp lệ là:

0, 1, 2

Nhưng điều kiện i <= length cho phép i = 3.

Khi đó:

hangDoiXeCho[3]

trả về:

undefined

Dẫn đến bảng LED hiển thị:

STT 4: undefined
Cách sửa

Sử dụng:

for (let i = 0; i < hangDoiXeCho.length; i++) {
    console.log(STT ${i + 1}: ${hangDoiXeCho[i]});
}

5. Bảng Test Cases
Trường hợp kiểm thử	Dữ liệu đầu vào	Kết quả sai thực tế	Kết quả đúng mong đợi
1. Hàng đợi có 3 xe và thêm 1 xe mới	['30A-98765', '29B-12345', '51C-45678'], xe mới 43D-88888	pop() lấy 51C-45678; vòng lặp có thêm STT 4: undefined	shift() lấy 30A-98765; danh sách còn 29B-12345, 51C-45678, 43D-88888
2. Hàng đợi có 1 xe	['30A-98765'], xe mới 43D-88888	pop() lấy xe đầu tiên nhưng sai logic FIFO; vòng lặp <= length có thể in thêm undefined	shift() lấy 30A-98765; push() thêm 43D-88888; chỉ hiển thị đúng 1 xe đang chờ
