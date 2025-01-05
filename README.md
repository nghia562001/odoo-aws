# odoo-aws-setup
Step-by-step guide to deploying Odoo Server on AWS

Cài đặt môi trường
----

**Cập nhật các gói phần mềm trong `Ubuntu`, chạy các lệnh sau:**

```bash
$ sudo apt update
```

**Cài đặt công cụ quản lý mã nguồn `git`, chạy các lệnh sau:**

```bash
$ sudo apt install git -y
```

**Cài đặt `Python` và `pip`, chạy các lệnh sau:**

```bash
$ sudo apt install python3-pip -y
```

**Cài đặt các `Dependencies` cần thiết cho `Python`, chạy các lệnh sau:**

```bash
$ sudo apt install -y build-essential wget python3-dev python3-venv python3-wheel libfreetype6-dev libxml2-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less libjpeg-dev zlib1g-dev libpq-dev libxslt1-dev libldap2-dev libtiff5-dev libjpeg8-dev libopenjp2-7-dev liblcms2-dev libwebp-dev libfribidi-dev libxcb1-dev
```

**Tạo mới `user` cho hệ thống, chạy các lệnh sau:**

```bash
$ sudo adduser odoo
```

📋 **Thông tin user**
> - **password:** `123456`
> - **Full Name []:** odoo
> - **Room Number []:** 1
> - **Work Phone []:** _(không có)_
> - **Home Phone []:** _(không có)_
> - **Other []:** _(không có)_

**Cài đặt `WKHTMLTOPDF`, chạy các lệnh sau:**

```bash
$ wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.0g-2ubuntu4_amd64.deb
$ sudo dpkg -i libssl1.1_1.1.0g-2ubuntu4_amd64.deb
```

Cài đặt và cấu hình Postgresql
----

**Cài đặt và khởi động cơ sở dữ liệu `PostgreSQL`, chạy các lệnh sau:**

```bash
$ sudo apt install postgresql postgresql-contrib -y
$ sudo systemctl start postgresql
$ sudo systemctl enable postgresql
```

**Cấu hình cơ sở dữ liệu `PostgreSQL`, chạy các lệnh sau:**

```bash
$ sudo passwd postgres
$ su - postgres
$ createuser odoo
$ psql
postgres# ALTER USER odoo WITH CREATEDB;
postgres# \q
exit;
```

Cài đặt và cấu hình Odoo 18
----

**Tạo `thư mục` và thiết lập `quyền` cho `Odoo`, chạy các lệnh sau:**

```bash
$ sudo mkdir -p /opt/odoo/odoo
$ sudo chown -R odoo /opt/odoo
$ sudo chgrp -R odoo /opt/odoo
```

**Chuyển sang `user odoo` và cài đặt `Odoo 18`, chạy các lệnh sau:**

```bash
$ sudo su - odoo
odoo@ip-172-31-15-222:~$ git clone https://www.github.com/odoo/odoo --depth 1 --branch 18.0 /opt/odoo/odoo
odoo@ip-172-31-15-222:~$ cd /opt/odoo
```

**Tạo và khởi động môi trường ảo `Virtual Environment`, chạy các lệnh sau:**

```bash
odoo@ip-172-31-15-222:/opt/odoo$ python3 -m venv odoo-venv
odoo@ip-172-31-15-222:/opt/odoo$ source odoo-venv/bin/activate
```

**Cài đặt các `Dependencies` cần thiết cho `Odoo`, chạy các lệnh sau:**
```bash
(odoo-venv) odoo@ip-172-31-15-222:/opt/odoo$ pip3 install wheel
(odoo-venv) odoo@ip-172-31-15-222:/opt/odoo$ pip3 install -r odoo/requirements.txt
```

**`Deactivate` môi trường ảo `Virtual Environment`, chạy các lệnh sau:**
```bash
(odoo-venv) odoo@ip-172-31-15-222:/opt/odoo$ deactivate
```

**Tạo thư mục `Addons`, chạy các lệnh sau:**
```bash
odoo@ip-172-31-15-222:/opt/odoo$ mkdir /opt/odoo/odoo-custom-addons
odoo@ip-172-31-15-222:/opt/odoo$ exit
```

**Tạo file cấu hình `Configuration` cho `Odoo`, chạy các lệnh sau:**
```bash
$ sudo nano /etc/odoo.conf
```

📋 **Nội dung file cấu hình**
>[options]
>
>admin_passwd = 123456
>
>db_host = False
>db_port = False
>
>db_user = odoo
>db_password = False
>
>addons_path = /opt/odoo/odoo/addons,/opt/odoo/odoo-custom-addons

**Tạo file dịch vụ `Service` cho `Odoo`, chạy các lệnh sau:**
```bash
$ sudo nano /etc/systemd/system/odoo.service
```

📋 **Nội dung file dịch vụ**
>[Unit]
>
>Description=Odoo
>Requires=postgresql.service
>After=network.target postgresql.service
>
>[Service]
>
>Type=simple
>SyslogIdentifier=odoo
>PermissionsStartOnly=true
>
>User=odoo
>Group=odoo
>
>ExecStart=/opt/odoo/odoo-venv/bin/python3 /opt/odoo/odoo/odoo-bin -c /etc/odoo.conf
>StandardOutput=journal+console
>
>[Install]
>
>WantedBy=multi-user.target

**Khởi động hệ thống, chạy các lệnh sau:**
```bash
$ sudo systemctl daemon-reload
$ sudo systemctl start odoo
$ sudo systemctl enable odoo
```

**Kiểm tra trạng thái `status`, chạy các lệnh sau:**
```bash
$ sudo systemctl status odoo
```
