B1. Đưa dự án cần deploy lên server (Qua git clone/ SFTF)
Tài nguyên thực hiện:
GitHub - DevOpsBBUN/Session06_Demo1
GitHub - DevOpsBBUN/Session06_Demo2

Đường dẫn lưu trữ trên server demo:
/home/tranvohuutai/projects/

Kiểm tra tất cả luồng hiện tại trên nginx
ls -l /etc/nginx/sites-enabled/

B2. sudo vào cấu hình nginx
sudo nano /etc/nginx/sites-available/Session06_Demo1
#Lưu ý về tên đường dẫn, dự án tên gì thì đổi thành tên đấy

#Cấu hình Nginx
server {
    listen 8081; 
    server_name _;

    root /home/tranvohuutai/projects/Session06_Demo1;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

#Lưu ý về listen (port) và root (đường dẫn đến dự án cần deploy trên server)
#Lặp lại bước 2 đối với các dự án khác

B3. Tạo một shortcut từ thư mục sites-available sang thư mục sites-enabled:
sudo ln -s /etc/nginx/sites-available/Session06_Demo1 /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/Session06_Demo2 /etc/nginx/sites-enabled/        

Kiểm tra nginx
sudo nginx -t
# Nếu hiện ra 2 dòng "is ok" và "is successful" là được. Nếu có lỗi sẽ hiển thị lên trên, thường sẽ có các lỗi về trùng port,...


B4. restart nginx để nhận cấu hình mới
sudo systemctl restart nginx

B5. Mở ufw
sudo ufw allow 8081/tcp
sudo ufw allow 8082/tcp

sudo ufw reload

B6. Kiểm tra thành quả
Lên web search
http://<ip>:<port>