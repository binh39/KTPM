FROM debian:bookworm-slim

# Cài đặt SSH server, sudo, VNC server, và các công cụ cơ bản
RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    tightvncserver \
    xterm \
    && apt-get clean

# Đặt mật khẩu cho root
RUN echo 'root:root123' | chpasswd

# Tạo user 'binh' với mật khẩu 'binh123' và cấp quyền sudo
RUN useradd -m -s /bin/bash binh && echo "binh:binh123" | chpasswd
RUN usermod -aG sudo binh

# Cấu hình SSH
RUN mkdir /var/run/sshd
RUN echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config
RUN echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config
RUN echo 'AllowUsers binh root' >> /etc/ssh/sshd_config

# Thiết lập mật khẩu VNC cho người dùng 'binh'
# Sử dụng một tệp đầu vào để cung cấp mật khẩu hai lần.
RUN echo "vnc123\nvnc123" | su - binh -c 'vncpasswd'

# Thiết lập file khởi động X cho VNC
RUN echo '#!/bin/sh\n\n' > /home/binh/.vnc/xstartup && chmod +x /home/binh/.vnc/xstartup
