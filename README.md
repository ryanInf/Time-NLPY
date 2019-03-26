## 说明：  
Time-NLP的python3版本，由于原作者sunfiyes的是python2版本，无法在python3上使用，故修改部分代码，使其可在Python3上使用（本人新手，可能有bug）
原项目地址：https://github.com/sunfiyes/Time-NLPY  

## 安装方式：  
1) cd到当前目录
2) python setup.py install

PS~ ：
window下可能出现安装regex错误，可到
https://www.lfd.uci.edu/~gohlke/pythonlibs/#regex
下载对应版本的regex手动安装。

## 使用方法
将中文时间描述转换为三种标准的时间格式的时间字符串：
1) 时间点（timestamp，表示某一具体时间时间描述）; 
2) 时间量（timedelta，表示时间的增量的时间描述）; 
3) 时间区间（timespan，有具体起始和结束时间点的时间区间）。

示例：
``` python
from TimeNormalizer import TimeNormalizer # 引入包

tn = TimeNormalizer()

res = tn.parse(target='从明天到明年', timeBase='2013-02-28 16:30:29') # target为待分析语句，timeBase为基准时间默认是当前时间
print(res)
res = tn.parse(target='2013年二月二十八日下午四点三十分二十九秒', timeBase='2013-02-28 16:30:29') # target为待分析语句，timeBase为基准时间默认是当前时间
print(res)
res = tn.parse(target='我需要大概33天2分钟', timeBase='2013-02-28 16:30:29') # target为待分析语句，timeBase为基准时间默认是当前时间
print(res)
res = tn.parse(target='1月末') # target为待分析语句，timeBase为基准时间默认是当前时间
res = tn.parse(target='明天')
js = json.loads(res)
print(js)
print(res)
```
输出：
```
{"timespan": ["2013-03-01 00:00:00", "2014-01-01 00:00:00"], "type": "timespan"}
{"timestamp": "2013-02-28 16:30:29", "type": "timestamp"}
{"timedelta": "33 days, 0:02:00", "type": "timedelta"}
{'timestamp': '2019-03-27 00:00:00', 'type': 'timestamp'}
{"timestamp": "2019-03-27 00:00:00", "type": "timestamp"}
```
调用示例见Test.py

关于节假日的增加方法：  
1) 在resource目录下的holi_lunar(阴历)或holi_solar(阳历)文件内按照格式加入新增的节日名称和日期
2) 在resource目录下的regex.txt文件内加入相应节日的正则匹配，并删除regex.pkl缓存文件
3) 在TimeUnit类中的norm_setHoliday方法同样加入节日的正则匹配
