# escape=`

FROM mcr.microsoft.com/windows/nanoserver:1809
ENV HOMEDRIVE c:
ENV HOMEPATH \Users\ContainerUser
ADD erlang21.2.tar.gz c:\
ADD rabbitmq_server-3.7.10.tar.gz c:\
ENV ERLANG_HOME c:\erlang
ENV RABBITMQ_HOME c:\rabbitmq_server
RUN reg add HKCU\Environment && setx PATH %PATH%;c:\rabbitmq_server\sbin
ENV RABBITMQ_LOGS=- RABBITMQ_SASL_LOGS=-
RUN md %APPDATA%\RabbitMQ && echo loopback_users.guest = false >> %APPDATA%\RabbitMQ\rabbitmq.conf
EXPOSE 4369 5671 5672 25672
RUN rabbitmq-plugins enable --offline rabbitmq_management
EXPOSE 15671 15672
CMD ["C:\\rabbitmq_server\\sbin\\rabbitmq-server.bat"]
