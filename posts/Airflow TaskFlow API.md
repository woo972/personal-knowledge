---
tags:
  - dev
  - airflow
  - batch
dg-publish: true
---
- airflow 2.0부터 도입된 데이터 파이프라인
- 주로 간단한 작업에 사용되는 것 같다 (operator의 경우BranchpythonOperator, Pythonoperator, DockerOperator, KubernetesOperators 등에서만 사용 가능)
- DAG 인스턴스화는 필수
```python
@dag(...)
def sample_dag()
```
- Task는 @task() decorator를 정의하여 사용한다. task 간의 dependencies는 순차 호출을 통해 실행한다
```python
@task()
def extract():
...
@task(multiple_outputs=True)
def transform(order_data_dict: dict):
...
@task()
def load(total_order_value: float):
...
order_data = extract()
order_summary = transfrom(order_data)
load(order_summary["total_order_value"])
```
- dag를 run하려면 @dag()로 정의한 함수를 호출한다
```python
sample_dag()
```
- 각 @task()로 설정된 task들은 argument overriding을 통해 재사용이 가능하다
```python
@task
def add_task(x, y):
	print(f"Task args: x=(x>, y=fy)")
	return x + y

@dag(start_date=datetime(2022, 1, 1))
def mydag():
	start = add_task.override(task_id="start")(1, 2)
	for i in range(3):
		start >> add_task.override(task_id=f"add_start_(i)")(start, i)
		
@dag(start_date=datetime(2022, 1, 1))
def mydag2():
	start = add_task(1, 2)
	for i in range(3):
		start>> add_task.override(task_id=f"new_add_task_fi)")(start, i)
		
first_dag = mydag()
second_dag = mydag2()
```
- 기존 방식의 job과 디펜던시 설정도 가능하다
```python
result = xxOperator()

@task()
def someTask():
...

final = someTask()

result >> final
```
