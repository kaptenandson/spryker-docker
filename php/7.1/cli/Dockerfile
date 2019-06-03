ARG FROM_REGISTRY
ARG FROM_IMAGE_NAME

FROM $FROM_REGISTRY/$FROM_IMAGE_NAME:7.1

MAINTAINER Daniel Rose <daniel-rose@gmx.de>

RUN ln -s /usr/local/bin/php /usr/bin/php

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["php"]
