## Basic Shell Script

스크립트 실행파일의 첫 줄에 **#!** 으로 시작하는 코드가 있다. 영어로는 Sharp(#) + Bang(!)의 합성어로 **sha-bang** 이라고 표현한다.<br>
##### #!은 2Byte의 매직넘버로 해당 스크립트를 실행시켜줄 프로그램의 경로를 지정하는 역할이다.
```bash
#!/usr/bin/bash/env bash
```

##### Hello world 출력
```bash
#!/usr/bin/env bash
echo "hello world"
# echo는 자동으로 줄바꿈을 실행한다.
printf "hello world"
printf "%s hello world" yo!
```

##### Comments
```bash
# # 기호로 시작하면 주석으로 인식한다.
```

##### Functions
```bash
# function을 생략해도 된다.
# 호출은 반드시 선언 이후에 이루어져야 한다.
function test(){
  echo "test"
}

test

```

##### Variables
```bash
# Global Var
string="hey, what's up?"
echo ${string}

test(){
  # Local Var
  local string="local"
  echo ${string}
}
```

##### Array Variables
```bash
# declare -a는 생략 가능
declare -a array

array=("oasis", "nirvana", "radiohead", "coldplay")

array[4]="weezer"

${array[@]} #배열 전체
${#array[@]} #배열 전체 개수 출력

array=(${array[@]})

# 특정 index 지우기
unset array[4]

# 전체 지우기
unset array
```

##### Variables Revisited
```bash
declare -r str #readonly

declare -i number=10 #integer

declare -a array #array
```

##### for, if..elif
```bash
for string in "nirvana" "oasis" "keane"; do;
  echo ${string};
done

str1="hello"
str2="world"

if [ ${str1} == ${str2} ]; then
  echo "hello world"
elif [ ${str1} == ${str3} ]; then
  echo "go away"
else
  echo "good bye"
fi
```

##### User Input
```bash
echo Hello, what\'s your name?
read varname
echo It\'s nice to meet you $varname

# -p prompt, -sp silent input
echo Hello, what\'s your name?
read -p varname
read -sp password
echo It\'s nice to meet you $varname
```
