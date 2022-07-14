SELECT

COLUMN_NAME AS'列名',
IS_NULLABLE AS'允许为空',
DATA_TYPE AS'数据类型',
COLUMN_COMMENT AS'字段说明'FROM information_schema.COLUMNS

WHERE TABLE_NAME= 'table'


https://blog.csdn.net/weixin_31304817/article/details/113149466
