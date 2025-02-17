* CÔNG NGHỆ CỦA DỰ ÁN:

- Backend sử dụng framework Django
- Frontend sử dụng framework ReactJs
- Database sử dụng PostgreSQL

* HƯỚNG DẪN CHẠY DỰ ÁN.

I. Tạo môi trường ảo trước!!!!

1. Ae cài file requirements.txt vào env của ae nha
2. Kích hoạt môi trường ảo lên 

(HÃY CHẮC CHẮN RẰNG MỌI HOẠT ĐỘNG VỀ SAU ĐỀU ĐƯỢC CHẠY TRONG MÔI TRƯỜNG ẢO)

II> Tạo cơ sở dữ liệu trước nhé!

Dự án này sử dụng PostgreSQL làm cơ sở dữ liệu. Sau khi clone về, các bạn cần thực hiện các bước sau để cấu hình và chạy được dự án trên máy của mình.

1. Nếu bạn chưa cài đặt PostgreSQL, hãy thực hiện theo hướng dẫn dưới đây:

Trên Ubuntu:
Mở Terminal và chạy:

sudo apt update
sudo apt install postgresql postgresql-contrib

Trên Windows:
Truy cập PostgreSQL Download Page và tải về trình cài đặt.
Chạy trình cài đặt và làm theo hướng dẫn trên màn hình.

Sau khi run file .exe của PostgreSQL xong, ta đã hoàn thành việc cài PostgreSQL vào máy

2. Tiếp theo, bạn cần tạo một tài khoản user mới và database mới của PostgreSQL cho dự án này (Nghĩa là mỗi bạn clone về sẽ phải tự tạo database riêng cho máy bạn). Hãy thực hiện theo các bước sau:

Mở Command Prompt lên. Sau đó, chạy lệnh: 

psql -U postgres 

để chạy PostgreSQL với quyền admin. 

3. Sau đó, tạo cơ sở dữ liệu mới bằng dòng lệnh sau đây:

CREATE DATABASE your_database_name; // ví dụ thay your_database_name thành todo_database

Vậy đã hoàn tất việc tạo database PostgreSQL trên máy của bạn. Hãy lưu ý tên database này để sử dụng trong các bước tiếp theo.

4. Kế tiếp, bạn sẽ tạo tài khoản user. Hãy chạy lệnh sau:

CREATE USER your_username WITH PASSWORD 'your_password';

your_username sẽ là tên tài khoản của bạn, và your_password sẽ là mật khẩu của bạn. Ví dụ, bạn có thể tạo tài khoản với tên là "todo_user" và mật khẩu là "todo_password". Vậy là bạn đã hoàn thành việc tạo user và database trong PostgreSQL.

5. Việc cần làm cuối cùng là cấp quyền cho người dùng trên cơ sở dữ liệu bằng câu lệnh sau:

GRANT ALL PRIVILEGES ON DATABASE your_database_name TO your_username;

Và ta phải kết nối vào database đã tạo bằng câu lệnh sau đây:

\c your_database_name

Sau đó, cấp quyền trên schema public bắng câu lệnh này:

GRANT ALL PRIVILEGES ON SCHEMA public TO your_username;

GRANT ALL PRIVILEGES ON SCHEMA public TO todo_user;

Cuối cùng, gõ lệnh sau để thoát khỏi PostgreSQL:

\q

Xong, bạn đã tạo thành công cơ sở dữ liệu và tài khoản người dùng cho dự án của mình.

6. Vậy làm sao để dự án hiểu được bạn sẽ sử dụng database và user của PostgreSQL bạn vừa tạo? 
Bạn sẽ phải thêm thông tin về cơ sở dữ liệu và người dùng vào file setting.py của dự án. Hãy thêm các dòng sau vào file setting.py:
(file setting.py nằm ở Backend/todo_backend/setting.py)

DATABASES = {
    'default': {
         'ENGINE': 'django.db.backends.postgresql',
         'NAME': 'ten_database_cua_ban',
         'USER': 'ten_user_cua_ban',
         'PASSWORD': 'mat_khau_cua_ban',
         'HOST': 'localhost',
         'PORT': '5432',
    }
}

7. Chưa xong đâu, sau khi cấu hình cơ sở dữ liệu trong file settings.py, bước tiếp theo là kết nối Django với cơ sở dữ liệu PostgreSQL và thiết lập các bảng cần thiết. Để thực hiện, chúng ta sử dụng hai lệnh quan trọng đó là makemigrations và migrate. 

Django sẽ chuẩn bị các file migration để mô tả cách tạo bảng. Hãy chạy câu lệnh sau:
Lưu ý, lệnh dưới đây cần phải được chạy trong thư mục chứa file manage.py.
(Nên bạn hãy cd đến thư mục Backend vì thư mục này chứa file manage.py)

python manage.py makemigrations

Sau khi tạo file migration, cần áp dụng chúng lên cơ sở dữ liệu PostgreSQL. Chạy lệnh sau:

python manage.py migrate

Xong!!!!! Bạn đã xong bước cài csdl cho dự án. Vậy là chạy dự án được rồi nhé. Cách chạy như sau:

p/s: vì ta sử dụng hai framework riêng biệt cho backend và frontend (backend sử dụng Django, frontend sử dụng ReactJs).
Nên nếu sử dụng terminal thì cần phải có 2 terminal chạy song song cùng lúc. (Hoặc nếu sử dụng Command Prompt thì phải mở hai tab
chạy cùng lúc)

II> Chạy dự án

1. Chạy server backend

Ở terminal đầu tiên:

p/s: đừng quên rằng phải chạy trong môi trường ảo của bạn vừa tạo nhaa!

Chúng ta đang đứng tại vị trí sau: \ToDoList-WebApp
Chúng ta sẽ đi đến: cd Backend
Ở vị trí này ta chạy lệnh:

python manage.py runserver

2. Chạy frontend

Ở terminal thứ hai (chạy song song với terminal đầu tiên):

Chúng ta hãy cd đến thư mục Frontend
Sau đó, cd đến thư mục todo_frontend
Ở đây, chạy lệnh:

npm install

Tiếp theo, bạn chạy lệnh này là có thể chạy được frontend của project:

npm start















