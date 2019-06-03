FROM php:7.2-cli-stretch

MAINTAINER Daniel Rose <daniel-rose@gmx.de>

COPY docker-entrypoint.sh /usr/local/bin/

RUN ln -s /usr/local/bin/php /usr/bin/php

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["php"]