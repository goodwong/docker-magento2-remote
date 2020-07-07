FROM docker-magento2-php-fpm

# copied from official composer Dockerfile
RUN curl -s -f -L -o /tmp/installer.php https://install.phpcomposer.com/installer \
    && php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer \
    && composer --ansi --version --no-interaction \
    && rm -rf /tmp/* /tmp/.htaccess

# www-data的home目录权限有问题，所以需要自行创建并添加权限
RUN whoami && mkdir -p /var/www/.composer/ && chown -R www-data:www-data /var/www/

RUN apt-get update && apt-get install -y git

# php 内存
RUN cp $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini \
    && echo "memory_limit = 1024M" >> $PHP_INI_DIR/conf.d/memory_limit.ini

USER www-data

#RUN if [ ${CHANGE_SOURCE} = 'CN' ]; then \
#    # Change composer to china source \
#    echo "change to Chinese composer source"; \
#    composer config -g repo.packagist composer https://packagist.phpcomposer.com \
#;fi

# 将magento加入命令列表
ENV PATH=$PATH:/workspace/bin

ENTRYPOINT []