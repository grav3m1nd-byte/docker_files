# Faraday Dockerfile

This is a custom Faraday Dockerfile based on Ubuntu 20.04 as the image from Faradaysec did not work for me.
This Dockerfile is set to use a local postgresql instance and volumes.
The volumes to mount should be:
  /local_path/Faraday/database:/var/lib/postgresql/12/main
  /local_path/Faraday/faraday:/home/faraday
  
## To build the image:
```sudo docker build --build-arg username=your_username -t grav3m1nd/faraday-server:latest <local_path_to_Dockerfile>```

## Next steps after running the image:
### Run it:
![image](https://user-images.githubusercontent.com/54182057/111835518-70f86e00-88cb-11eb-8d65-324721ce1ce1.png)

### Locally:
```ssh your_username@127.0.0.1 -p 2022```

### In the Docker instance:
```
$ sudo faraday-manage initdb
$ sed -i "s/bind_address \= localhost/bind_address \= 0\.0\.0\.0/g" /home/faraday/.faraday/config/server.ini

$ sudo /opt/faraday/bin/faraday-server &
```
