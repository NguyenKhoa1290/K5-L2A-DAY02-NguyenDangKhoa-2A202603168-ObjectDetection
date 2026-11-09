# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe chở người cá nhân, có dạng nhỏ/nhẹ, thân thấp và thường là sedan, hatchback, SUV, taxi, hoặc xe bán tải nhỏ. | Không dùng cho xe buýt lớn, xe tải hàng, mô tô; nếu là xe bán tải/cabin nhỏ nhưng hình dáng giống xe con thì vẫn là `car`. |
| `truck` | Xe tải chở hàng, xe đầu kéo, xe container hoặc xe có thùng/cabin dài, thể hiện rõ mục đích vận chuyển hàng hóa. | Dựa vào thùng hàng, cabin dài, khung tải; không gán cho SUV, minivan hay xe chở người thông thường. |
| `bus` | Xe buýt, xe chở khách có thân dài, nhiều cửa kính và không gian chở người theo tuyến. | Dạng thân dài, cao, nhiều cửa sổ; khác với van và xe con vì rõ chức năng chở khách công cộng. |
| `van` | Xe van, minivan chở hàng hoặc chở người, có thân chữ nhật/khối, không phải xe con hay xe buýt. | Van giao hàng, minivan, xe tải nhỏ nhưng không phải dạng thùng hàng kiểu `truck`; khác với `bus` vì thân ngắn hơn và không mang tính chở khách tuyến. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: nên đặt box khép kín phần vật thể nhìn thấy, không quá rộng quá hở, và giữ gần với mép ngoài nhất để tối đa hóa độ chính xác khi đánh giá IoU.
- Vật thể bị che khuất: nếu phần nhìn thấy đủ rõ để nhận diện loại xe (car/truck/bus/van), vẫn đánh nhãn; chỉ cần bao phủ phần còn thấy, không cần suy đoán phần bị che.
- Vật thể bị cắt bởi rìa ảnh: vẫn giữ box nếu phần vật thể hiện lên đủ để nhận diện, nhưng chỉ chứa phần có trong khung hình; không kéo box ra ngoài ảnh.
- Vật thể rất nhỏ/mơ hồ: nếu không đủ rõ để phân biệt lớp, ưu tiên bỏ qua hoặc gán theo mức độ chắc chắn cao nhất; không đánh nhãn theo cảm tính khi hình ảnh quá mờ hoặc quá nhỏ.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_...` | Xe SUV/xe con ở xa, chỉ thấy phần thân và kính xe nhưng không rõ thùng hàng | `car` | Hình dáng mô tả xe chở người, không có đặc điểm thùng hàng hay thân dài của `truck`; phù hợp với schema `car` khi phần nhìn thấy đủ để nhận diện. |
| `drive_...` | Van giao hàng hoặc minivan chở hàng ở góc nghiêng | `van` | Xe có khung cao, hình hộp/van rõ hơn xe con, nhưng không có nhiều cửa kính dài và tính chất chở khách tuyến như `bus`. |
| `drive_...` | Xe tải/cabin có thùng hàng rõ hoặc đầu kéo dài | `truck` | Thùng hàng, cabin dài hoặc khung xe chuyên chở hàng là đặc điểm chính của `truck`; không nên xếp vào `car` nếu có hình dáng hàng hóa rõ ràng. |
