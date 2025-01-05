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

**Tạo mới `user` cho hệ thống , chạy các lệnh sau:**

```bash
$ sudo adduser odoo
```

> 📋 **Thông tin user**
>
> - **password:** `123456`
> - **Full Name []:** odoo
> - **Room Number []:** 1
> - **Work Phone []:** _(không có)_
> - **Home Phone []:** _(không có)_
> - **Other []:** _(không có)_

Cài đặt và cấu hình Postgresql
----
