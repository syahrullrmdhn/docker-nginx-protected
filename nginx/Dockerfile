FROM nginx:stable

# Install ModSecurity dan dependensinya
RUN apt-get update && \
    apt-get install -y libmodsecurity3 libnginx-mod-http-ndk libnginx-mod-http-modsecurity && \
    apt-get clean

# Aktifkan modul ModSecurity
RUN ln -s /usr/share/modsecurity-crs /etc/modsecurity/crs

# Copy konfigurasi Nginx dan ModSecurity
COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf
COPY ../modsecurity/modsecurity.conf /etc/modsecurity/modsecurity.conf
COPY ../modsecurity/crs-setup.conf /etc/modsecurity/crs-setup.conf
COPY ../modsecurity/crs/rules /etc/modsecurity/crs/rules

# Buat direktori log
RUN mkdir -p /var/log/nginx && chmod -R 755 /var/log/nginx

# Enable ModSecurity dan load CRS
RUN sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/modsecurity/modsecurity.conf
