docker run -it archlinux:latest
docker ps -a 
docker export "id" | gzip > /mnt/c/temp/archlinux.tar.gz


wsl --import arch c:\wsl\archlinux c:\temp\archlinux.gz