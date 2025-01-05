# odoo-aws-setup
Step-by-step guide to deploying Odoo Server on AWS

Cài đặt môi trường
----

> **Cập nhật các gói phần mềm trong `Ubuntu`, chạy các lệnh sau:**

```bash
$ sudo apt update
```

> **Cài đặt công cụ quản lý mã nguồn `git`, chạy các lệnh sau:**

```bash
$ sudo apt install git -y
```

> **Cài đặt `python` và `pip`, chạy các lệnh sau:**

```bash
$ sudo apt install python3-pip -y
```

> **Cài đặt các `thư viện` cần thiết cho `python`, chạy các lệnh sau:**

```bash
$ sudo apt install -y build-essential wget python3-dev python3-venv python3-wheel libfreetype6-dev libxml2-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less libjpeg-dev zlib1g-dev libpq-dev libxslt1-dev libldap2-dev libtiff5-dev libjpeg8-dev libopenjp2-7-dev liblcms2-dev libwebp-dev libfribidi-dev libxcb1-dev
```
