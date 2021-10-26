# Some Log
## 21-06-01
### mysql创建触发器
-- ----------------------------

-- 创建insert触发器(当用户上报报修后就形成报表记录)

-- ----------------------------

CREATE TRIGGER ng_service_insert AFTER INSERT ON ng_service FOR EACH ROW 

BEGIN

IF(NEW.type<>0 && NEW.state<>14) THEN

SET @report_insert_name = (SELECT name FROM ng_app_user WHERE id = NEW.create_user);

SET @report_insert_phone = (SELECT phone FROM ng_app_user WHERE id = NEW.create_user);

SET @report_insert_customer = (SELECT customer FROM ng_battery WHERE bid = NEW.bid);

SET @report_insert_area_one = (SELECT area_one FROM view_battery_china WHERE bid = NEW.bid);

SET @report_insert_idea = (SELECT idea FROM ng_service_deal_idea WHERE id = NEW.idea);

SET @report_insert_type = (SELECT type FROM ng_battery WHERE bid = NEW.bid);

SET @report_insert_time = (SELECT time FROM ng_battery WHERE bid = NEW.bid);

SET @report_insert_app_value = (SELECT app_value FROM ng_service_state WHERE id = NEW.state);

SET @report_insert_number =   (SELECT number FROM ng_service_cdj_building WHERE service_id = NEW.id);

SET @report_insert_deal_time = (SELECT create_time FROM ng_exception_analysis_result WHERE service_id = NEW.id ORDER BY create_time LIMIT 1);

-- SET @report_remark = (SELECT remark FROM ng_exception_analysis_result WHERE service_id = NEW.id  ORDER BY remark LIMIT 1);

 SET @report_insert_remark = (SELECT  GROUP_CONCAT(remark) FROM ng_exception_analysis_result WHERE service_id IN (SELECT id FROM ng_exception_analysis_result WHERE service_id = NEW.id ));
 
-- SET @report_temp_exception_id =  (SELECT b FROM ng_exception_analysis_result WHERE service_id = NEW.id ORDER BY b LIMIT 1);

-- SET @report_info = (SELECT info FROM ng_exception WHERE id = @report_temp_exception_id);

SET @report_insert_info =  (SELECT GROUP_CONCAT(info) FROM ng_exception WHERE id IN (SELECT b FROM ng_exception_analysis_result WHERE service_id = NEW.id GROUP BY b));

SET @report_insert_finish_time = (SELECT time FROM ng_service_process WHERE state=12 AND service_id=NEW.id ORDER BY time DESC LIMIT 1);

SET @report_insert_new_bid = (SELECT new_bid FROM ng_send_new_battery_task WHERE state<>-1 AND sid=NEW.id ORDER BY id DESC LIMIT 1);

SET @report_insert_wlnumber = (SELECT number FROM view_battery_china WHERE bid = NEW.id);

SET @report_insert_cdjtype = (SELECT info FROM ng_more_info_description WHERE id = NEW.id);

INSERT INTO ng_report (id,bid,name,phone,create_time,address,customer,area_one,idea,type,time,app_value,number,deal_time,remark,info,finish_time,new_bid,wlnumber,cdjtype)

VALUES(NEW.id,NEW.bid,@report_insert_name,@report_insert_phone,NEW.create_time,NEW.address,@report_insert_customer,@report_insert_area_one,@report_insert_idea,@report_insert_type,@report_insert_time,
@report_insert_app_value,@report_insert_number,@report_insert_deal_time,@report_insert_remark,@report_insert_info,@report_insert_finish_time,@report_insert_new_bid,@report_insert_wlnumber,@report_insert_cdjtype);

END IF;

END

-- ----------------------------

-- 创建update触发器(报表信息随报修记录动态变动)

-- ----------------------------

CREATE TRIGGER ng_service_update AFTER UPDATE ON ng_service FOR EACH ROW 

BEGIN

IF(NEW.type<>0 && NEW.state<>14) THEN

--    IF(NEW.state=12) THEN

--    SLEEP(1)

--    END IF;

SET @report_update_name = (SELECT name FROM ng_app_user WHERE id = NEW.create_user);

SET @report_update_phone = (SELECT phone FROM ng_app_user WHERE id = NEW.create_user);

SET @report_update_customer = (SELECT customer FROM ng_battery WHERE bid = NEW.bid);

SET @report_update_area_one = (SELECT area_one FROM view_battery_china WHERE bid = NEW.bid);

SET @report_update_idea = (SELECT idea FROM ng_service_deal_idea WHERE id = NEW.idea);

SET @report_update_type = (SELECT type FROM ng_battery WHERE bid = NEW.bid);

SET @report_update_time = (SELECT time FROM ng_battery WHERE bid = NEW.bid);

SET @report_update_app_value = (SELECT app_value FROM ng_service_state WHERE id = NEW.state);

SET @report_update_number =   (SELECT number FROM ng_service_cdj_building WHERE service_id = NEW.id);

SET @report_update_deal_time = (SELECT create_time FROM ng_exception_analysis_result WHERE service_id = NEW.id ORDER BY create_time LIMIT 1);

-- SET @report_remark = (SELECT remark FROM ng_exception_analysis_result WHERE service_id = NEW.id  ORDER BY remark LIMIT 1);

 SET @report_update_remark = (SELECT  GROUP_CONCAT(remark) FROM ng_exception_analysis_result WHERE service_id IN (SELECT id FROM ng_exception_analysis_result WHERE service_id = NEW.id ));
 
-- SET @report_temp_exception_id =  (SELECT b FROM ng_exception_analysis_result WHERE service_id = NEW.id ORDER BY b LIMIT 1);

-- SET @report_info = (SELECT info FROM ng_exception WHERE id = @report_temp_exception_id);

SET @report_update_info =  (SELECT GROUP_CONCAT(info) FROM ng_exception WHERE id IN (SELECT b FROM ng_exception_analysis_result WHERE service_id = NEW.id GROUP BY b));

SET @report_update_finish_time = (SELECT time FROM ng_service_process WHERE state=12 AND service_id=NEW.id ORDER BY time DESC LIMIT 1);

SET @report_update_new_bid = (SELECT new_bid FROM ng_send_new_battery_task WHERE state<>-1 AND sid=NEW.id ORDER BY id DESC LIMIT 1);

SET @report_update_wlnumber = (SELECT number FROM view_battery_china WHERE bid = NEW.id);

SET @report_update_cdjtype = (SELECT info FROM ng_more_info_description WHERE id = NEW.id);

UPDATE ng_report

SET 

bid = NEW.bid,

name = @report_update_name,

phone = @report_update_phone,

address = NEW.address,

customer = @report_update_customer,

area_one = @report_update_area_one,

idea = @report_update_idea,

type =  @report_update_type,

time = @report_update_time,

app_value =@report_update_app_value,

number = @report_update_number,

deal_time = @report_update_deal_time,

remark = @report_update_remark,

info = @report_update_info,

finish_time = @report_update_finish_time,

new_bid = @report_update_new_bid,

wlnumber = @report_update_wlnumber,

cdjtype = @report_update_cdjtype

WHERE id = NEW.id;

END IF;

END

--------------------------------------------------------------------------------------------------------------------------
## 21-06-04  
### mysql数据库创建root用户
-- CREATE USER 'yangshen'@'%' IDENTIFIED BY '123456';  

-- grant all privileges on *.* to 'yangshen'@'%' IDENTIFIED BY '123456';

## 21-06-08
###  pip更换源
python -m pip install --upgrade pip太慢

输入：

python -m pip install --upgrade pip  -i http://pypi.douban.com/simple --trusted-host pypi.douban.com

其他下载链接：

豆瓣(douban) http://pypi.douban.com/simple/

阿里云 http://mirrors.aliyun.com/pypi/simple/

中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/

清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/

中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/

anaconda 环境中pip install 第三方库下载较慢；

pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pandas

## 21-06-29
### PHP Model 连接不同数据库
    protected $table = 'test';

//    protected $connection = 'mysql://root:@127.0.0.1:3306/test#utf8';

//    protected $connection = [

//        // 数据库类型

//        'type'        => 'mysql',

//        // 数据库连接DSN配置

//        'dsn'         => '',

//        // 服务器地址

//        'hostname'    => 'ip',

//        // 数据库名

//        'database'    => 'test',

//        // 数据库用户名

//        'username'    => 'root',

//        // 数据库密码

//        'password'    => '',

//        // 数据库连接端口

//        'hostport'    => '3306',

//        'params'      => [],

//        // 数据库编码默认采用utf8

//        'charset'     => 'utf8',

//        // 数据库表前缀

//        'prefix'      => 'my_',

//    ];

```
    protected function initialize(){

        parent::initialize();

        $this->connection = config("dbConfig");
    }
```
'dbConfig' =>[

    // 数据库类型

    'type'           => 'mysql',

    // 服务器地址

    'hostname'    => 'ip',

    // 数据库名

    'database'    => 'test',

    // 数据库用户名

    'username'    => 'root',

    // 数据库密码

    'password'    => '',
 
    // 端口

    'hostport'       => '3306',
 
    // 连接dsn
  
    'dsn'            => '',
   
    // 数据库连接参数
  
    'params'         => [],
 
    // 数据库编码默认采用utf8
  
    'charset'        => 'utf8',
   
    // 数据库表前缀
   
    'prefix'         => 'ng_',
   
    // 数据库调试模式
   
    'debug'          => true,
   
    // 数据库部署方式:0 集中式(单一服务器),1 分布式(主从服务器)
   
    'deploy'         => 0,
   
    // 数据库读写是否分离 主从式有效
   
    'rw_separate'    => false,
   
    // 读写分离后 主服务器数量
   
    'master_num'     => 1,
   
    // 指定从服务器序号
   
    'slave_no'       => '',
   
    // 是否严格检查字段是否存在
   
    'fields_strict'  => true,
   
    // 数据集返回类型 array 数组 collection Collection对象
   
    'resultset_type' => 'array',
   
    // 是否自动写入时间戳字段
   
    'auto_timestamp' => false,
   
    // 是否需要进行SQL性能分析
   
    'sql_explain'    => false,
   
    //取消前台自动格式化
   
    'datetime_format' => false,



## 21-07-08
### pyinstaller
使用pyinstaller程序打包，import pymssql 的程序时，有如下提示ModuleNotFoundError: No module named 'pymssql._mssql'
尝试了网上的方法 import _mssql 或者 import pymssql._mssql 等都没解决，最终尝试如下方法解决：
import pymssql后，添加这几行即可
```python
from pymssql import _mssql
from pymssql import _pymssql
import uuid
import decimal
```
如果不行的话，升级pip、pyinstaller等之后，再pyinstaller -F xxx.py ,更新pip: python -m pip install --upgrade pip --trusted-host pypi.org

pymssql安装

pip install --trusted-host pypi.org pymssql

新版本的python集成环境 不需要--trusted-host pypi.org也可

## 21-07-16
###  查询更换电池已完成，报修单据还未完成
SELECT  

t.id,t.sid,t.new_bid,s.bid,s.bid_check,s.state,sp.state,sp.time

FROM ng_send_new_battery_task t

LEFT JOIN ng_service s ON s.id =t.sid

LEFT JOIN ng_service_process sp ON sp.service_id=s.id

WHERE t.state = 3  AND s.state <>12

ORDER BY sid,time

## 21-10-08
### 翻译测试
```python
import requests

while True:
    string = input("请输入一段要翻译的文字")
    data = {'doctype': 'json', 'type': 'AUTO', 'i': string}
    url = 'http://fanyi.youdao.com/translate'
    r = requests.get(url, params=data)
    result = r.json()
    print('result=', result)
    print(result['translateResult'][0][0]['tgt'])

## 请输入一段要翻译的文字我爱你
## result= {'type': 'ZH_CN2EN', 'errorCode': 0, 'elapsedTime': 0, 'translateResult': [[{'src': '我爱你', 'tgt': 'I love you'}]]}
## I love you

```

## 21-10-26
### python生成pdf
安装wkhtmltopdf
https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf
安装pdfkit
```python
pip install pdfkit
```
代码
```python
pip install pdfkit
```
```python
# yshen
# 2021/10/26 8:58
import pdfkit

# PDF中包含的文字
content = '这是一个测试页面。' + '<br>' + 'Hello World! 你好，世界!'

html = '<html><head><meta charset="UTF-8"></head>' \
       '<body><div align="center"><p>%s</p></div></body></html>' % content

# 转换为PDF
pdfkit.from_string(html, 'test.pdf')
```
