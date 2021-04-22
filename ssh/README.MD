# docker-ssh
## dockerfile 
```
RUN apt-get -y install sudo curl openssh-client openssh-server vim

# set root login
RUN echo "root:root" | chpasswd
RUN sed -ri 's/^#PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config  
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config 

```
## docker run
### entrypoint
```
TOKEN='passwd123'
# 容器内jupyter代码存放路径，自行修改
JUPYTER_DIR="/code"
  
echo "总共参数: $#"
echo "脚本名字: $0"
service ssh start
nohup jupyter notebook --no-browser --ip=0.0.0.0 --allow-root --NotebookApp.token="$TOKEN" --notebook-dir="$JUPYTER_DIR" &
```
