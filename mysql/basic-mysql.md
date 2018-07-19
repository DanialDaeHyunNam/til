## Basic MySQL

- Ceil

```MySQL
select ceil(12.345)
output : 13

select ceil(12.345 * 10)*0.1 라는 방식으로 특정 자리 올림이 가능하다.
output : 12.4
```

- Round

```MySQL
select round(12.345, 2)
output : 12.35
```

- Truncate

```MySQL
select truncate(12.345, 1)
output: 12.3
```

- If

**IF(조건, 참인 경우 출력, 거짓인 경우 출력)**<br>
도시에 인구가 100만이 넘으면 big city, 그렇지 않으면 small city를 scale 컬럼에 출력<br>

```MySQL
select name, population, if(population > 1000000, "big city", "small city") as scale
from city
having scale = "small city"
order by population desc
```

- Ifnull

**IFNULL(컬럼명, 디폴트 데이터)**
독립연도가 없는 데이터를 0으로 출력

```MySQL
select indepyear, ifnull(indepyear, 0)
from country
```

- Case when then else end

나라별로 인구가 10억이상, 10억 ~ 1억 이상, 1억 이하 - "b", "m", "s"

```MySQL
select name, population,
case
	when population > 1000000000 then "b"
	when population > 100000000 then "m"
	else "s"
end as scale
from country
having scale="m"
order by population desc
```
- date_format

```MySQL
select date_format(payment_date, "%Y-%m") as monthly, sum(amount)
from payment
group by monthly
```

- JOIN : inner, left, right

```MySQL
join이라고만 쓰면 기본은 inner join
select *
from user
join addr
on user.user_id = addr.user_id

select user.user_id, user.name, addr.addr
from user
left join addr
on user.user_id = addr.user_id

select user.user_id, user.name, addr.addr, addr.user_id
from user
right join addr
on user.user_id = addr.user_id
```

- UNION : full outer

```MySQL
select user.name, addr.addr
from user
left join addr
on user.user_id = addr.user_id
union
select user.name, addr.addr
from user
right join addr
on user.user_id = addr.user_id

만약 union all을 넣으면 중복된것이 사라지지 않는다.
```

- sub-query

```MySQL
# select

# sub query : select, from, where 절 등에서 사용이 가능하다.
# 전체 나라수, 도시수, 언어수를 하나의 row로 출력

select
(select count(*) from country) as country_cnt,
(select count(*) from city) as city_cnt,
(select count(distinct(language)) from countrylanguage) as language_cnt
from dual # from dual은 생략 가능

------------------------------------------------------------------

# from

# 먼저 필터링을 하기때문에 1:1 매핑되는 join구문에서 훨씬 적은 양의 일을 하게된다.
# 포인트는 join때 최대한 적은 데이터가 작동되게하는게 좋다.
select city.countrycode, city.name, country.name, city.population
from(
select countrycode, name, population
from city
where population > 8000000
) as city
join country
on city.countrycode = country.code

# 아래와 위는 같은 결과를 낸다.
select city.countrycode, city.name, country.name, city.population
from city
join country
on city.countrycode = country.code
having city.population > 8000000

------------------------------------------------------------------

# where

select code, name, headofstate
from country
where code in (
  select countrycode from city where population > 8000000
)
```

- index : explain
```MySQL
# select 속도를 높이지만, 저장공간을 많이 차지한다는 단점이 있다.
# 또한, 새로 생성된 저장공간에도 항상 싱크를 맞추기때문에 insert시간도 길어진다.

create index salaries
on salaries (salary)
```

- view
```
# view : 가상의 테이블 - 컬럼의 수정이나, 인덱설정 같은 명령을 할 수 없다.

select *
from countrylanguage
join
code_name
/* select country.code, country.name as country_name, city.name as city_name
from country
join city
on country.code = city.countrycode */
on code_name.code = countrylanguage.countrycode

create view code_name as
select country.code, country.name as country_name, city.name as city_name
from country
join city
on country.code = city.countrycode
```
