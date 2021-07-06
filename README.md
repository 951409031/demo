# beluga-connector
微念关键词实时数据

## 目前支持平台级功能
|    | 联想词 | 搜索结果 | 热榜 |
| :---: | :---: | :---: | :---: |
| weibo | √ |  |  |
| baidu | √ |
| bilibili-pc | √ |
| xiaohongshu | √ |

## 接口说明
### 1.联想词
> /suggestion

*请求方式: GET*

**请求参数**

| 参数名 | 类型 | 内容        | 必要性 | 备注 |
| ------ | ---- | ----------- | ------ | ---- |
| platform | str  | weibo | 必要   | 平台名称 |
| word | str | 李子柒 | 必要 | 搜索词 |

**返回示例**
```json
{
    "code": 200, 
    "msg": "成功",
    "data": {
        "words": ["李子柒螺狮粉", "李子柒视频"]
    }
}
```

## 返回说明
```json
{
    "code": {
        "成功": 200,
        "参数缺失": 401, 
        "参数错误": 402,
        "网络错误": 501,
        "解析失败": 502
    },
    "msg": {
        "成功": "成功",
        "参数缺失": "参数缺失: word", 
        "参数错误": "参数错误: {'platform': 'bili'}",
        "网络错误": "网络错误, 请求失败",
        "解析失败": "网页结构变化, 解析失败"
    },
    
    "data": {}
}
```
> data 包含实际内容, 错误时为 {}

## 测试
```shell
// 启动 server
python3 index.py
```
```shell
// 运行测试代码
python3 test/suggestion.py
```

## 日志
```sql
CREATE TABLE IF NOT EXISTS `beluga`(
    `id` INT AUTO_INCREMENT COMMENT 'id, 主键',
    `ip` VARCHAR(20) COMMENT '客户端 ip',
    `ua` VARCHAR(100) COMMENT '客户端 ua',
    `path` VARCHAR(20) NOT NULL COMMENT '请求路由',
    `query` VARCHAR(100) NOT NULL COMMENT '请求参数',
    `response` TEXT NOT NULL COMMENT '响应内容',
    `time` DATETIME COMMENT '请求时间',
    PRIMARY KEY (`id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

# 配置
- secret
```json
{
  "mysql": {
    "host": "127.0.0.1",
    "user": "",
    "password": "",
    "database": "",
    "port": 3306
  }
}
```
 
