🚀 Guía de Instalación y Configuración: DNS y Nginx
📋 Índice

🔧 Instalación de DNS
🌐 Instalación de Nginx
⚙️ Configuración DNS
🔨 Configuración Nginx
🔗 Integración DNS + Nginx
✅ Verificación y Testing


🔧 Instalación de DNS
📦 Instalación de BIND9 (Ubuntu/Debian)
bash# Actualizar repositorios
sudo apt update

# Instalar BIND9 y utilidades
sudo apt install bind9 bind9utils bind9-doc

# Verificar instalación
systemctl status bind9
🐧 Instalación en CentOS/RHEL
bash# Instalar BIND
sudo yum install bind bind-utils

# O en versiones más recientes
sudo dnf install bind bind-utils

# Habilitar y iniciar servicio
sudo systemctl enable named
sudo systemctl start named
📁 Estructura de Archivos DNS
/etc/bind/
├── named.conf           # 📄 Configuración principal
├── named.conf.local     # 🏠 Zonas locales
├── named.conf.options   # ⚙️ Opciones globales
└── zones/              # 📂 Archivos de zona
    ├── db.example.com
    └── db.192.168.1

🌐 Instalación de Nginx
📦 Ubuntu/Debian
bash# Actualizar repositorios
sudo apt update

# Instalar Nginx
sudo apt install nginx

# Iniciar y habilitar servicio
sudo systemctl start nginx
sudo systemctl enable nginx

# Verificar estado
sudo systemctl status nginx
🐧 CentOS/RHEL
bash# Instalar Nginx
sudo yum install nginx
# O para versiones recientes
sudo dnf install nginx

# Iniciar servicios
sudo systemctl start nginx
sudo systemctl enable nginx

# Configurar firewall
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
📁 Estructura de Archivos Nginx
/etc/nginx/
├── nginx.conf              # 📄 Configuración principal
├── sites-available/        # 📂 Sitios disponibles
├── sites-enabled/          # 🔗 Sitios habilitados
├── conf.d/                # ⚙️ Configuraciones adicionales
└── /var/www/html/         # 🌐 Directorio web por defecto

⚙️ Configuración DNS
🔧 Configuración Principal (/etc/bind/named.conf.options)
bindoptions {
    directory "/var/cache/bind";
    
    // 🌍 Configurar forwarders (DNS públicos)
    forwarders {
        8.8.8.8;
        8.8.4.4;
        1.1.1.1;
    };
    
    // 🔒 Configuraciones de seguridad
    allow-recursion { localhost; 192.168.1.0/24; };
    allow-query { localhost; 192.168.1.0/24; };
    
    // 📡 IPv6
    listen-on-v6 { any; };
    
    // 🚫 Deshabilitar transferencias de zona
    allow-transfer { none; };
};
🏠 Configuración de Zonas (/etc/bind/named.conf.local)
bind// 📍 Zona directa
zone "example.com" {
    type master;
    file "/etc/bind/zones/db.example.com";
};

// 🔄 Zona inversa
zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/zones/db.192.168.1";
};
📝 Archivo de Zona Directa (/etc/bind/zones/db.example.com)
bind$TTL    604800
@       IN      SOA     ns1.example.com. admin.example.com. (
                        2024052701      ; Serial
                        604800          ; Refresh
                        86400           ; Retry
                        2419200         ; Expire
                        604800 )        ; Negative Cache TTL

; 🏷️ Servidores de nombres
@       IN      NS      ns1.example.com.

; 📍 Registros A
ns1     IN      A       192.168.1.10
www     IN      A       192.168.1.20
web     IN      A       192.168.1.20
mail    IN      A       192.168.1.30

; 📧 Registro MX
@       IN      MX      10 mail.example.com.

; 🔗 Registro CNAME
ftp     IN      CNAME   www.example.com.
🔄 Archivo de Zona Inversa (/etc/bind/zones/db.192.168.1)
bind$TTL    604800
@       IN      SOA     ns1.example.com. admin.example.com. (
                        2024052701      ; Serial
                        604800          ; Refresh
                        86400           ; Retry
                        2419200         ; Expire
                        604800 )        ; Negative Cache TTL

; 🏷️ Servidor de nombres
@       IN      NS      ns1.example.com.

; 🔄 Registros PTR
10      IN      PTR     ns1.example.com.
20      IN      PTR     www.example.com.
30      IN      PTR     mail.example.com.

🔨 Configuración Nginx
🏠 Sitio Web Principal (/etc/nginx/sites-available/default)
nginxserver {
    # 🎯 Puerto y nombre del servidor
    listen 80;
    listen [::]:80;
    server_name example.com www.example.com;
    
    # 📂 Directorio raíz
    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;
    
    # 📍 Configuración de ubicaciones
    location / {
        try_files $uri $uri/ =404;
    }
    
    # 📊 Logs
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    
    # 🔒 Seguridad básica
    server_tokens off;
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header X-Content-Type-Options "nosniff" always;
}
🔐 Configuración HTTPS (/etc/nginx/sites-available/example.com-ssl)
nginxserver {
    # 🔒 SSL/TLS
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name example.com www.example.com;
    
    # 📜 Certificados SSL
    ssl_certificate /etc/ssl/certs/example.com.crt;
    ssl_certificate_key /etc/ssl/private/example.com.key;
    
    # 🔐 Configuración SSL
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:DHE-RSA-AES256-GCM-SHA512;
    ssl_prefer_server_ciphers off;
    
    # 📂 Directorio raíz
    root /var/www/html;
    index index.html index.htm;
    
    location / {
        try_files $uri $uri/ =404;
    }
}

# 🔄 Redirección HTTP a HTTPS
server {
    listen 80;
    listen [::]:80;
    server_name example.com www.example.com;
    return 301 https://$server_name$request_uri;
}
⚡ Configuración de Proxy Reverso
nginxupstream backend {
    server 192.168.1.100:8080;
    server 192.168.1.101:8080;
}

server {
    listen 80;
    server_name app.example.com;
    
    location / {
        proxy_pass http://backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

🔗 Integración DNS + Nginx
1️⃣ Configurar Registros DNS para Nginx
bind; En el archivo de zona DNS
www     IN      A       192.168.1.20    ; 🌐 Servidor web principal
app     IN      A       192.168.1.20    ; 📱 Aplicación web
api     IN      A       192.168.1.20    ; 🔌 API
static  IN      A       192.168.1.21    ; 📁 Contenido estático
2️⃣ Configurar Virtual Hosts en Nginx
bash# 📁 Crear directorios para cada sitio
sudo mkdir -p /var/www/example.com/html
sudo mkdir -p /var/www/app.example.com/html

# 🔗 Habilitar sitios
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/app.example.com /etc/nginx/sites-enabled/

✅ Verificación y Testing
🔍 Verificar DNS
bash# 🧪 Probar configuración DNS
sudo named-checkconf
sudo named-checkzone example.com /etc/bind/zones/db.example.com

# 🔄 Reiniciar servicios DNS
sudo systemctl restart bind9

# 🎯 Probar resolución
nslookup www.example.com localhost
dig @localhost example.com
🌐 Verificar Nginx
bash# 🧪 Probar configuración
sudo nginx -t

# 🔄 Recargar configuración
sudo systemctl reload nginx

# 📊 Ver estado
sudo systemctl status nginx

# 📝 Ver logs
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
🔧 Comandos de Troubleshooting
bash# 🔍 DNS Troubleshooting
sudo netstat -tulpn | grep :53
sudo journalctl -u bind9 -f

# 🌐 Nginx Troubleshooting
sudo netstat -tulpn | grep :80
sudo netstat -tulpn | grep :443
curl -I http://example.com
curl -I https://example.com

🎯 Testing Final
✅ Checklist de Verificación

 🔧 DNS resuelve correctamente los dominios
 🌐 Nginx responde en puerto 80 y 443
 🔒 Certificados SSL funcionando
 📍 Virtual hosts configurados correctamente
 🔄 Redirecciones HTTP → HTTPS activas
 📊 Logs funcionando correctamente
 🔥 Firewall configurado apropiadamente

🎪 Comandos de Testing
bash# 🧪 Test completo de conectividad
curl -v http://www.example.com
curl -v https://www.example.com
curl -v http://app.example.com

# 🔍 Test de DNS desde diferentes servidores
dig @8.8.8.8 example.com
dig @1.1.1.1 example.com
dig @192.168.1.10 example.com  # Tu servidor DNS
