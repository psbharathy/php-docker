# php-docker

# Build the PHP 7.1 image
docker build -t php71-fpm .

# Run the PHP container with shared volume
docker run -d --name php71-fpm -v /var/www/html:/var/www/html -p 9000:9000 php71-fpm

# Edit Apache Virtual Host Configuration
  # Configure Apache to use PHP-FPM running in the container /etc/httpd/conf.d/welcome.conf or /etc/apache2/sites-available/000-default.conf
    <FilesMatch "\.php$">
        SetHandler "proxy:fcgi://127.0.0.1:9000"
    </FilesMatch>
# restart apache
sudo systemctl restart apache2
