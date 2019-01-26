# escape=`

FROM mcr.microsoft.com/windows/servercore:ltsc2019

ADD http://erlang.org/download/otp_win64_21.2.exe c:\download\otp_win64_21.2.exe
RUN start /w c:\download\otp_win64_21.2.exe /S /D=c:\erlang
ENV ERLANG_HOME c:\erlang

ADD https://www.7-zip.org/a/7z1806-x64.exe c:\download\7z1806-x64.exe
RUN start /w c:\download\7z1806-x64.exe /S /D="c:\7zip"

ADD https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.7.10/rabbitmq-server-windows-3.7.10.zip c:\download\rabbitmq-server-windows-3.7.10.zip
RUN c:\7zip\7z.exe x c:\download\rabbitmq-server-windows-3.7.10.zip
ENV RABBITMQ_HOME c:\rabbitmq_server-3.7.10
# get logs to stdout
ENV RABBITMQ_LOGS=- RABBITMQ_SASL_LOGS=-
RUN RMDIR /S /Q download
RUN setx PATH %PATH%;%RABBITMQ_HOME%\sbin
RUN  md %APPDATA%\RabbitMQ && echo loopback_users.guest = false >> %APPDATA%\RabbitMQ\rabbitmq.conf
EXPOSE 4369 5671 5672 25672
CMD ["C:\\rabbitmq_server-3.7.10\\sbin\\rabbitmq-server.bat"]