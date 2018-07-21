## Run python flask on EC2 in the backgroud

 Flask 프레임워크를 사용하여 구현한 Python 어플리케이션을 AWS EC2에서 프로세스가 계속 실행되게 하려면

 ```linux
 nohup python app.py &

 # & 을 뒤에 붙이면 이 어플리케이션을 Background에서 실행시키라는 의미이다.
 ```
