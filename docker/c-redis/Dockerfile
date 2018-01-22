FROM redis:4.0.6-alpine

# for docker-compose mode (TODO проблема с configs)
COPY /docker/c-redis/redis.conf /usr/local/etc/redis/redis.conf

CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]