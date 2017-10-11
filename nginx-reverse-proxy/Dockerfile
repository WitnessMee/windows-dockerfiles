# Build: docker build -t esko/nginx .
# Run:   docker run -d -p 80:80 -p 443:443 nginx_proxy esko/nginx
FROM microsoft/windowsservercore

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ARG NgInxVersion="1.13.5"
ENV NgInxZipUrl="http://nginx.org/download/nginx-${NgInxVersion}.zip"

RUN Invoke-WebRequest -Uri $env:NgInxZipUrl -UseBasicParsing -Outfile c:\\nginx.zip
RUN Expand-Archive -Path c:\\nginx.zip -DestinationPath c:

WORKDIR "c:\\nginx-${NgInxVersion}"

COPY ./nginx.conf conf\\nginx.conf
COPY ./proxy.conf conf\\proxy.conf
COPY ./_.esko.com.crt conf\\_.esko.com.crt
COPY ./_.esko.com.key conf\\_.esko.com.key

ENTRYPOINT powershell .\\nginx.exe