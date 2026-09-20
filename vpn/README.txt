# 1. Переходим в рабочую директорию OpenVPN (где создавалась PKI сервера)
cd /etc/openvpn

# 2. Указываем в качестве временной папки стандартный системный /tmp
export EASYRSA_TEMP_DIR="/tmp"

# 3. Запускаем генерацию, указав полный путь к исполняемому скрипту
/usr/share/easy-rsa/3/easyrsa --batch gen-req Dima nopass

# подписать сертификат клиента следующей
/usr/share/easy-rsa/3/easyrsa --batch sign-req client Dima

# /bin/cp -v /etc/openvpn/pki/ca.crt /etc/openvpn/ta.key /etc/openvpn/pki/private/Dima.key /etc/openvpn/pki/issued/Dima.crt  /tmp/
tar -cvf dima.tar ca.crt Dima.* ta.key

# с vpn узла подключаюсь к proxy
screen -> autossh -M 0 -N -D 0.0.0.0:9898 root@ip_proxy_за_границей
