# ベースイメージを設定
FROM mysql:8.0

# DB設定
ENV MYSQL_DATABASE=laravel_local \
  MYSQL_USER=phper \
  MYSQL_PASSWORD=secret \
  MYSQL_ROOT_PASSWORD=secret \
  TZ=Asia/Tokyo

# my.cnfをマウント
COPY ./my.cnf /etc/mysql/conf.d/my.cnf

# パーミッション設定
RUN chmod 644 /etc/mysql/conf.d/my.cnf