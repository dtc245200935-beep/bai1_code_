<<<<<<< HEAD
# BasicWebApi – luyện kỹ thuật Minimal API (Bài 1, PI 1.2)

Ví dụ của giáo trình mục 1.2: một API nhỏ để học cấu trúc solution, hosting model trong `Program.cs`,
endpoint GET/POST, nhận dữ liệu từ route / query string / body / DI và trả kết quả bằng `Results`.

## Tự tạo lại từ đầu

```bash
dotnet new sln -n BasicWebApi --format slnx
dotnet new webapi -n BasicWebApi -o src/BasicWebApi --no-openapi
dotnet sln BasicWebApi.slnx add src/BasicWebApi/BasicWebApi.csproj
```

Sau đó xóa code mẫu trong `src/BasicWebApi/Program.cs` và viết lại theo file trong thư mục này.

## Chạy

```bash
dotnet build
dotnet run --project src/BasicWebApi --urls http://localhost:5081
```

Kiểm thử bằng `requests.http` (VS Code REST Client) hoặc:

```powershell
curl.exe http://localhost:5081/
curl.exe "http://localhost:5081/hello/An?language=en"
```

| Request | Kết quả mong đợi |
|---|---|
| `GET /` | 200, `{"application":"BasicWebApi",...}` |
| `GET /hello/An?language=en` | 200, `{"message":"Hello, An!"}` |
| `POST /greetings {"name":"Binh"}` | 201, header `Location: /greetings/1`, JSON có `id, name, createdAt` |
| `POST /greetings {"name":""}` | 400, `{"message":"Name must not be empty."}` |
=======
# MiniDistributedSystem – EduSubmit, lát cắt 1

Hai tiến trình độc lập giao tiếp qua HTTP (MEP yêu cầu–phản hồi):

- `src/Submission.Api` – máy chủ, Minimal API trên ASP.NET Core (.NET 10)
- `src/Submission.Client` – máy khách dòng lệnh dùng `HttpClient`

## Tự tạo lại từ đầu bằng .NET CLI

```bash
mkdir MiniDistributedSystem && cd MiniDistributedSystem
dotnet new sln -n MiniDistributedSystem
dotnet new web -n Submission.Api -o src/Submission.Api
dotnet new console -n Submission.Client -o src/Submission.Client
dotnet sln add src/Submission.Api/Submission.Api.csproj
dotnet sln add src/Submission.Client/Submission.Client.csproj
```

## Chạy

Terminal 1 (API):

```bash
dotnet run --project src/Submission.Api --urls http://localhost:5000
```

Terminal 2 (Client):

```bash
dotnet run --project src/Submission.Client -- http://localhost:5000
```

Kết quả mong đợi:

```
Danh sach bai tap:
- 1: Bai tap 1
- 2: Bai tap 2
Da nop bai. Ma luot nop: <guid>
Trang thai: received
```

Có thể thử từng endpoint bằng `requests.http` (VS Code REST Client / Visual Studio) hoặc `curl`.

## Bài tập

1. Thêm bài tập mẫu thứ 3 và kiểm tra máy khách in đúng.
2. Tắt API rồi chạy máy khách: ghi lại lỗi và giải thích.
3. Gửi thiếu `StudentCode`/`RepositoryUrl`: quan sát 400 Bad Request.
4. (Mở rộng) Thêm `GET /api/submissions/{id}` và cho máy khách tra cứu lại lượt nộp.
>>>>>>> ef482739b47aec2c207733df3afd01749f937f11
