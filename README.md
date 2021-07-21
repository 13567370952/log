# Some Log

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
//        // 数据库连接参数
//        'params'      => [],
//        // 数据库编码默认采用utf8
//        'charset'     => 'utf8',
//        // 数据库表前缀
//        'prefix'      => 'my_',
//    ];

    protected function initialize(){
        parent::initialize();
        $this->connection = config("dbConfig");
    }

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


## 21-07-28
### pyinstaller
使用pyinstaller程序打包，import pymssql 的程序时，有如下提示
ModuleNotFoundError: No module named 'pymssql._mssql'
尝试了网上的方法 import _mssql 或者 import pymssql._mssql 等都没解决，最终尝试如下方法解决：
import pymssql后，添加这几行即可
from pymssql import _mssql
from pymssql import _pymssql
import uuid
import decimal
如果不行的话，升级pip、pyinstaller等之后，再pyinstaller -F xxx.py
更新pip
python -m pip install --upgrade pip --trusted-host pypi.org
pymssql安装
pip install --trusted-host pypi.org pymssql
新版本的python集成环境 不需要--trusted-host pypi.org也可