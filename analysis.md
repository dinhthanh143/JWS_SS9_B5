BÁO CÁO GIẢI PHÁP: TRẢI NGHIỆM ĐA NGÔN NGỮ (I18N) TOÀN CẦU
1. Thiết kế Kiến trúc & Logic
   Sơ đồ luồng hoạt động (Data Flow)
   User Request: Người dùng truy cập URL kèm tham số, ví dụ: index?lang=jp.

Interceptor (LocaleChangeInterceptor): Spring MVC sẽ "đánh chặn" request này, quét tham số lang. Nếu thấy giá trị mới, nó sẽ kích hoạt bộ chuyển đổi ngôn ngữ.

LocaleResolver: Nhận giá trị từ Interceptor và tiến hành ghi đè ngôn ngữ hiện tại của người dùng.

View Rendering (Thymeleaf): Thymeleaf dựa vào Locale hiện tại để tìm từ khóa trong các file .properties tương ứng và render ra HTML.

Quyết định công cụ: CookieLocaleResolver
Lựa chọn: CookieLocaleResolver.

Lý do: Yêu cầu số 2 của Sếp là "Hôm sau vào lại vẫn phải nhớ".

SessionLocaleResolver sẽ bị xóa sạch khi khách đóng trình duyệt (Session chết).

CookieLocaleResolver lưu cấu hình trực tiếp xuống máy khách. Chúng ta có thể set thời gian sống (Max-Age) cho nó, đảm bảo khách quay lại sau 1 tuần hay 1 tháng thì web vẫn tự động hiển thị đúng tiếng Nhật/Hàn mà họ đã chọn.