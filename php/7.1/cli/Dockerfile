FROM php:7.1-cli-stretch

MAINTAINER Daniel Rose <daniel-rose@gmx.de>

RUN ln -s /usr/local/bin/php /usr/bin/php

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["php"]