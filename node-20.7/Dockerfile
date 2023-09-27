FROM    node:20.7-alpine

ENV     ENV=$ENV

USER    root
RUN     apk update --no-cache \
        && apk add --update --no-cache \
            autoconf \
            automake \
            build-base \
            gcc \
            libpng-dev \
            nasm \
            python3 \
            py3-pip \
            tzdata \
            vips-dev \
            zlib-dev \
        && npm install --location=global create-strapi-app@latest \
        && mkdir -p /app

WORKDIR /app


ENTRYPOINT  if [ ! -f "/app/package.json" ]; then \
                npx create-strapi-app@latest /app --quickstart --no-run --typescript \ 
                && npm install mysql --save; \
            fi \
            && npm install \
            && npm run build \
            && if [ $ENV = "dev" ]; then \
                npm run develop; \
            else \
                npm run start; \
            fi


EXPOSE  1337