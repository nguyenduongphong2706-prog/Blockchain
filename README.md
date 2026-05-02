# VOX_GOV Project

## Mô tả dự án

Dự án này là một hệ thống bầu chọn phiếu cho các môn học chuyên ngành trên blockchain Ethereum với một hợp đồng thông minh đơn giản và giao diện front-end đẹp mắt.

Nội dung chính:
- `contracts/Voting.sol`: hợp đồng thông minh Voting cho phép admin cấp quyền whitelist và người dùng đã được whitelist có thể bỏ phiếu cho các môn học.
- `frontend/index.html`: giao diện React đơn trang hiển thị danh sách môn học, biểu đồ và biểu mẫu bỏ phiếu.
- `scripts/deploy.js`: script triển khai hợp đồng lên mạng Hardhat.
- `test/Voting.test.js`: bộ test cơ bản kiểm tra tính năng khởi tạo ứng viên, whitelist và bỏ phiếu.

## Cấu trúc chính

- `contracts/`: chứa hợp đồng thông minh Solidity.
- `frontend/`: chứa giao diện web tĩnh.
- `scripts/`: chứa script deploy.
- `test/`: chứa test cho Hardhat.
- `hardhat.config.js`: cấu hình Hardhat.
- `package.json`: khai báo dev dependency và scripts.

## Cài đặt và chạy

1. Cài đặt dependency:

```bash
npm install
```

2. Biên dịch hợp đồng:

```bash
npx hardhat compile
```

3. Chạy mạng Hardhat cục bộ (nếu cần):

```bash
npx hardhat node
```

4. Triển khai hợp đồng lên mạng cục bộ:

```bash
npx hardhat run scripts/deploy.js --network localhost
```

5. Sao chép địa chỉ hợp đồng deploy được và dán vào `frontend/index.html` tại biến `CONTRACT_ADDRESS`.

## Sử dụng giao diện

1. Mở `frontend/index.html` bằng trình duyệt hoặc dựng một server tĩnh nếu cần.
2. Kết nối ví MetaMask từ giao diện.
3. Nếu bạn là owner, dùng khu vực quản trị để thêm các ví được phép vote vào whitelist.
4. Chọn một môn học và nhấn nút `Bỏ phiếu ngay`.
5. Sau khi vote thành công, giao diện sẽ cập nhật lại số liệu vote từ hợp đồng.

## Lưu ý quan trọng

- Giao diện hiện tại chỉ cập nhật số liệu sau khi thực hiện vote thành công.
- Dự án đã loại bỏ cơ chế tự động tăng số liệu ngẫu nhiên.
- Mỗi địa chỉ whitelist chỉ có thể bỏ phiếu một lần.
- Nếu muốn sử dụng giao diện thật, hãy đảm bảo giá trị của `CONTRACT_ADDRESS` đúng với hợp đồng deploy.

## Kiểm thử

Chạy test bằng Hardhat:

```bash
npx hardhat test
```

## Mở giao diện GUI

Chạy lệnh sau để mở được lệnh GUI

```bash
cd frontend
python3 -m http.server
```

## Tham khảo hợp đồng

Hợp đồng `Voting.sol` cung cấp các chức năng:
- `addToWhitelist(address)`: chỉ owner mới có thể thực hiện.
- `vote(uint256)`: người dùng whitelist bỏ phiếu cho ứng viên.
- `getAllCandidates()`: trả về danh sách ứng viên và số vote hiện có.
- `hasVoted(address)`: kiểm tra ví đã bầu chưa.
- `isWhitelisted(address)`: kiểm tra ví đã được cấp quyền chưa.
