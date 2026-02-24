FROM mariadb:11.4

# define o mantedor da imagem
LABEL maintainer="Guilherme"


# atualiza a imagem com os pacotes
RUN apt-get update && apt-get upgrade -y

# instal o perl 
RUN apt-get install libdbi-perl -y
RUN apt-get install libdatetime-perl -y
RUN apt-get install libdbd-mysql-perl -y

# cria o cron
RUN echo "1 0 * * * perl /usr/sbin/mysql_part.pl" > crontab -e

# Comando para iniciar o Mariadb no Container
#CMD ["mariadb", "-g", "daemon off;"]


