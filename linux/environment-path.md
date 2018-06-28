## Environment path

환경변수란 어떤 명령어(프로그램)을 직접 절대경로로 접근해서 실행하는것이아닌 어느 위치(디렉토리)에서든 명령어를 사용할 수 있게 하기위해서 설정하는 변수를 의미한다. <br>
즉, 만약 환경변수가 설정되어있지 않았다면 **ls** 와 같이 우리가 당연히 쓰는 쉘 명령어도 **/bin/ls** 라고 써야했던 것이다. 운영체제가 명령어를 찾는 순서는

<br>
**/etc/profile -> /etc/bashrc -> /etc/inputrc -> \$HOME/.bash_profile -> \$HOME/.bashrc -> \$HOME/.inputrc** 이런식이다.<br>
<br>
**export PATH=[경로]:\$PATH**



##### 용도

- **bashrc** : 주로 명령어를 간단히 하기위한 별명을 기록해둔다.

- **bash_profile** : 환경변수들이 들어간다.

- **bash_history** : 사용한 명령어가 기록.

- **bash_logout** : 로그아웃시 실행할 명령어를 기록하는 곳.

**bash_profile과 .bashrc의 차이** :<br> .bash_profile은 login shell이고 .bashrc는 not login shell. .bash_profile은 서버에 로그인 할때 실행이 되고, .bashrc는 새로운 쉘이 생성될때 실행이 된다.
