---
tags:
  - dev
  - batch
  - airflow
---
## DAG definition
---
- airflow를 활용하여 pipeline을 구축하기 위해서는 DAG definition 파일이 필요하다.
	- module import: dag, operator, datetime 등 필요한 module import
	- default argument: 각 태스크에서 사용될 생성자에 포함할 아규먼트를 정의
	- DAG 인스턴스화: DAG id 설정, 스케쥴 설정, argument 설정
	- Operator: 모든 operator는 airflow에서 작업을 수행하기 위해 필수적인 아규먼트를 포함하는 baseOperator를 상속한다. Bashoperator, PythonOperator 등이 있다. 특정 작업에는 [[Airflow TaskFlow API]]를 활용하는게 좋을 때도 있다
	- Task: operatpr를 dag에서 사용하기 위해서 task로 인스턴스화 해야한다. 각 operator에 task_id와 owner는 필수로 상속되거나 포함되어야 한다. (owner는 보통 default argument에서 정의할 듯)
- Templiting with Jinja:  Jinja templating를 활용해서 built-in 파라미터와 macro를 제공한다
```python
templated_command = dedent (
	"""
	{% for i in range(5) %}
		echo "{{ ds }}"
		echo "{{ macros.ds_add (ds, 7)}}"
	{% endfor %}
	"""
)

t3 = BashOperator(
	  task_id="templated",
	  depends_on_past=False,
	  bash_command=tempated_command,
)
```
## Dependencies 설정
---
```python
task1 >> task2
task2 >> [task2, task3]
```
## Testing
---
- Testing: airflow.cfg에 의해 참조되는 폴더에 DAG 파일이 있는 경우, 파싱 테스트를 아래와 같이 할 수 있다
```python
python ~/airflow/dags/tutorial.py
```
- metadata 테스트
```python
# initialize the database tables
airflow db init

# print the list of active DAGs
airflow dags list

# prints the list of tasks in the "tutorial" DAG
airflow tasks list tutorial

# prints the hierarchy of tasks in the "tutorial" DAG
airflow tasks list tutorial -tree
```
- local test (db에 상태저장 안됨)
```python
# command layout: command subcommand [dag_id] [task_id] [(optional) date)|

# testing print_date
airflow tasks test tutorial print_date 2015-06-01
```
- dag test
```
airflow dags test
```
## Date intervals
---
- airflow는 시간은 UTC로 맞춘다
- start_date = dag가 스케쥴링 되기 시작한 날 (date_interval의 처음 시작값 세팅)
- execution_date(-> logical-date, data_interval_start): dag의 id로 작동하는 값으로 date_interval의 시작값으로 세팅
- data_interval_end: 데이터 간격의 끝
- scheduling: crontab (얼마나 자주 작업을 수행할 것인가?)
- ex
	- start_date가 23년 6월 11일 일요일 9시
	- scheduling 이 매주 월요일 (=> 매주 1회이므로, 스케쥴 간격 7일)
	- 23년 6월 12일 월요일 9시에 작업 수행 안됨(스케쥴 간격 7일 미만)
	- 23년 6월 19일 월요일 9시에 최초 작업 수행
	- string 형식으로 datetime 가져오기: `{{macros.datetime.strftime(date_interval_start,'%Y%m%d')}}`
	- string 형식으로 datetime 시간추가 가져오기: `{{macros.datetime.strftime(date_interval_start + macros.timedelta(hours = 9),'%Y%m%d:%H%M%s') }}
## 재실행
---
#### catch up
- 마지막 data_interval로부터 그 이후 실행되지 않은 모든 data_interval 작업을 수행 (dag 정의시 catchup=False로 막을 수도 있음)
	- 아래와 같은 상황에서 airflow 데몬을 2016년 12월 2일 06시에 실행한 경우, 12월 1일~12월 2일 인터벌을 가진 DAG를 run하고, 12월 3일 00시에 12월 2일~12월 3일 인터벌을 가진 DAG run
	- 만일 catchup= True인 경우에는 2015년 12월 1일부터 2016년 12월 2일 까지 순차실행, , 12월 3일 00시에 12월 2일~12월 3일 인터벌을 가진 DAG run
```python
dag = DAG(
	"tutorial",
	default_args={
		"depends_on_past": True,
		"retries": 1,
		"retry_delay": datetime. timedelta(minutes=3),
	},
	start_date=pendulum.datetime(2015, 12, 1, tz="UTC"), 
	description="A simple tutorial DAG", 
	schedule="@daily", 
	catchup=False,
)
```
#### backfill
- 특정 기간동안의 work를 한번에 수행
- 특정 시점만 (심지어 start_date 이전이라도) 작업을 재수행하고 싶을 때 사용
```python
airflow dags backfill
--start-date START_DATE
--end-date END_DATE
dag_id
```
#### 재실행 task
- 실패한 작업을 재실행하기 위해서는 Clear를 통해 max_retries = 0, current instance state = None으로 세팅한 후에 한다
- 옵션
	- past: 가장 최근 data interval 전에 수행되는 태스크들
	- future: 가장 최근 data interval 후에 수행되는 태스크들
	- upstream: 현재 DAG의 upstream 태스크들
	- downstream: 현재 DAG의 downstream 태스크들
	- recursive: 부모/자식 DAG의 모든 태스크들
	- failed: 최근 수행된 DAG의 실패한 태스크들
## 기타
---
- Timezone: pendulum을 사용하라
