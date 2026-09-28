BÀI TẬP MÔN AN TOÀN VÀ BẢO MẬT THÔNG TIN

Họ và tên: Nguyễn Văn Tuyến

Bài 1. Tìm hiểu thuật toán mã hóa hiện đại DES và AES
1.1 Thuật toán DES
Khái niệm

DES (Data Encryption Standard) là thuật toán mã hóa đối xứng được IBM phát triển và được Hoa Kỳ sử dụng làm tiêu chuẩn mã hóa từ năm 1977.

Đặc điểm
Mã hóa đối xứng (một khóa dùng cho cả mã hóa và giải mã)
Độ dài khóa: 56 bit
Kích thước khối dữ liệu: 64 bit
Gồm 16 vòng mã hóa (Feistel Network)
Quy trình mã hóa
Chia dữ liệu thành từng khối 64 bit
Hoán vị ban đầu (Initial Permutation)
Thực hiện 16 vòng Feistel
Hoán vị cuối (Final Permutation)
Sinh bản mã
Quy trình giải mã

Giống quá trình mã hóa nhưng sử dụng khóa theo thứ tự ngược lại.

Ưu điểm
Thuật toán đơn giản
Tốc độ khá nhanh
Dễ cài đặt
Nhược điểm
Khóa chỉ 56 bit
Có thể bị tấn công vét cạn (Brute Force)
Không còn được khuyến nghị sử dụng
1.2 Thuật toán AES
Khái niệm

AES (Advanced Encryption Standard) là chuẩn mã hóa được NIST lựa chọn thay thế DES vào năm 2001.

Đây là thuật toán mã hóa đối xứng được sử dụng rộng rãi hiện nay.

Đặc điểm
Thuộc tính	AES
Loại	Đối xứng
Kích thước khối	128 bit
Độ dài khóa	128 / 192 / 256 bit
Số vòng	10 / 12 / 14
Quy trình mã hóa AES

Bước 1:

Thêm khóa ban đầu (AddRoundKey)

↓

Bước 2:

Lặp nhiều vòng gồm

SubBytes
ShiftRows
MixColumns
AddRoundKey

↓

Bước cuối

SubBytes
ShiftRows
AddRoundKey

↓

Sinh Ciphertext

Quy trình giải mã AES

Thực hiện các bước ngược lại:

InvShiftRows
InvSubBytes
AddRoundKey
InvMixColumns

Lặp lại đến khi thu được dữ liệu ban đầu.

Ưu điểm
Bảo mật rất cao
Tốc độ nhanh
Được sử dụng trong:
HTTPS
VPN
WiFi WPA2
Ngân hàng
Chính phủ
Nhược điểm
Cần chia sẻ khóa bí mật trước
Nếu lộ khóa thì toàn bộ dữ liệu bị giải mã
1.3 Cài đặt AES bằng Python
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad, unpad

key = b'1234567890123456'

cipher = AES.new(key, AES.MODE_ECB)

text = "Hello AES"

encrypted = cipher.encrypt(pad(text.encode(),16))

print("Encrypted:", encrypted)

cipher2 = AES.new(key, AES.MODE_ECB)

decrypted = unpad(cipher2.decrypt(encrypted),16)

print("Decrypted:", decrypted.decode())
Kết quả
Encrypted:
b'...'

Decrypted:
Hello AES
Bài 2. Thuật toán mã hóa bất đối xứng RSA
Khái niệm

RSA là thuật toán mã hóa khóa công khai được Ronald Rivest, Adi Shamir và Leonard Adleman phát minh năm 1977.

RSA sử dụng:

Public Key (Khóa công khai)
Private Key (Khóa bí mật)
Nguyên lý sinh cặp khóa
Bước 1

Chọn hai số nguyên tố lớn

p
q
Bước 2

Tính

n = p × q
Bước 3

Tính

φ(n)=(p−1)(q−1)
Bước 4

Chọn số

e

Sao cho

1<e<φ(n)

và

gcd(e,φ(n))=1
Bước 5

Tính

d

e×d ≡1 mod φ(n)
Kết quả

Public Key

(e,n)

Private Key

(d,n)
Quy trình mã hóa

Người gửi

↓

Dùng Public Key

↓

Sinh Ciphertext

↓

Gửi dữ liệu

Quy trình giải mã

Người nhận

↓

Dùng Private Key

↓

Giải mã

↓

Plaintext

Ưu điểm
Không cần chia sẻ khóa bí mật
Bảo mật cao
Hỗ trợ chữ ký số
Nhược điểm
Chậm
Không phù hợp mã hóa dữ liệu lớn
Bài 3. Ứng dụng RSA
3.1 Xác thực người gửi (Digital Signature)

Người gửi

↓

Hash dữ liệu

↓

Mã hóa Hash bằng Private Key

↓

Gửi

Dữ liệu
Chữ ký số

Người nhận

↓

Dùng Public Key giải mã chữ ký

↓

Hash lại dữ liệu

↓

So sánh

Nếu giống nhau

→ Dữ liệu không bị sửa.

3.2 Xác thực người nhận

Người gửi dùng Public Key của người nhận để mã hóa.

Chỉ người nhận sở hữu Private Key mới giải mã được.

3.3 Xác thực cả hai

Kết hợp:

RSA để trao đổi khóa
RSA Signature để xác thực
AES để mã hóa dữ liệu

Đây là mô hình được sử dụng trong:

HTTPS
SSL/TLS
VPN
3.4 So sánh RSA và AES
Tiêu chí	AES	RSA
Loại khóa	Đối xứng	Bất đối xứng
Tốc độ	Rất nhanh	Chậm
Khóa	128/192/256 bit	2048/3072/4096 bit
Mã hóa dữ liệu lớn	Tốt	Không phù hợp
Trao đổi khóa	Không	Có
Chữ ký số	Không	Có
3.5 Vì sao kết hợp RSA và AES?

Trong thực tế, hầu hết các hệ thống bảo mật (HTTPS, TLS, VPN...) đều kết hợp hai thuật toán:

RSA dùng để trao đổi khóa AES một cách an toàn.
AES dùng để mã hóa toàn bộ dữ liệu vì có tốc độ rất nhanh.
RSA còn dùng để xác thực danh tính và tạo chữ ký số.

Nhờ đó hệ thống vừa đảm bảo tính bảo mật, tính xác thực và hiệu năng cao, khắc phục được nhược điểm khi chỉ sử dụng riêng RSA hoặc AES.

Kết luận
DES là thuật toán mã hóa đối xứng đời cũ, hiện không còn an toàn do độ dài khóa ngắn.
AES là chuẩn mã hóa đối xứng hiện đại, nhanh và được sử dụng rộng rãi.
RSA là thuật toán mã hóa bất đối xứng, thích hợp cho trao đổi khóa và chữ ký số.
Trong thực tế, các hệ thống bảo mật thường kết hợp RSA và AES để tận dụng ưu điểm của cả hai: RSA trao đổi khóa an toàn, AES mã hóa dữ liệu hiệu quả.
