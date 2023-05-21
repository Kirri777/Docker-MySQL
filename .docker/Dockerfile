#Deriving the latest base image
FROM mariadb:latest

# Any working directory can be chosen as per choice like '/' or '/home' etc
WORKDIR /app

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
    && "date"
