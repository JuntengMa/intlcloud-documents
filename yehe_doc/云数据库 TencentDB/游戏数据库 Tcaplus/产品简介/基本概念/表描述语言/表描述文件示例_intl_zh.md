## proto2 表描述文件示例
如下是一个符合 proto2 语法规范的表描述文件。

```
syntax = "proto2";                      // 指明符合 proto2 语法规范
package myTcaplusTable;                 // 自定义包名

import "tcaplusservice.optionv1.proto"; // 这个文件定义了 Tcaplus 表的一些公共信息，需要在您的表定义中被引用(import)

message player {  // 使用 message 定义表，message 名即表名

    // 必须是指定了主键选项（tcaplusservice.tcaplus_primary_key）的 message 才能被识别为一张 TcaplusDB 业务数据表，否则此 message 只是一个结构体
    // 主键选项指定了主键字段名列表，字段名用逗号分割，最多四个字段能够被指定为主键
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // tcaplusservice.tcaplus_index 选项指定 Tcaplus 索引
    // 每个索引所包含的索引键必须是主键，并且所有索引字段集合的交集不能为空
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    //option(tcaplusservice.tcaplus_sharding_key) = "uin"; 用户可以自己显式设置索引分片字段。如果用户不显式设置，系统将默认采用主键字段作为分片字段

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // 使用默认的 DefaultAesCipherSuite 加密函数，非必须设置选项
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; //设置加密密码字符串的 md5 值，非必须设置选项

    // 以下是表的字段定义
    // TcaplusDB 表支持以下的数据类型：
    // 非嵌套类型：int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // 嵌套类型：message
    // Tcaplus 支持 REQUIRED、OPTIONAL 和 REPEATED 作为字段修饰符

    // 主键字段 (最多4个)
    required int64 uin = 1;  // 主键字段必须被 required 类型修饰，并且不能是嵌套类型
    required string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // message 中 string 和 bytes 类型字段可以指定为加密字段，非必须设置选项
    required int32 region = 3;
    // 一张表最多只能包含4个主键字段

    // 普通值字段
    required int32 gamesvrid = 4; // 普通字段可以被 required、optional 或 repeated 类型修饰
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // repeated 修饰的字段需要指定 packed=true 选项
    optional bool is_available = 7 [default = false]; // optional 类型字段可以指定默认值
    optional pay_info pay = 8; // 值字段的类型可以是自定义的结构体类型
}

message pay_info { //使用 message 定义结构体

    required int64 pay_id = 1;
    optional uint64 total_money = 2;
    optional uint64 pay_times = 3;
    optional pay_auth_info auth = 4;

    message pay_auth_info { // 结构体类型支持嵌套定义
        required string pay_keys = 1;
        optional int64 update_time = 2;
    }
}
```


## proto3 表描述文件示例
如下是一个符合 proto3 语法规范的表描述文件。
```
syntax = "proto3";                      // 指明符合 proto3 语法规范
package myTcaplusTable;                 // 自定义包名

import "tcaplusservice.optionv1.proto"; // 这个文件定义了 Tcaplus 表的一些公共信息，需要在您的表定义中被引用(import)

message player {  // 使用 message 定义表，message 名即表名

    // 必须是指定了主键选项（tcaplusservice.tcaplus_primary_key）的 message 才能被识别为一张 TcaplusDB 业务数据表，否则此 message 只是一个结构体
    // 主键选项指定了主键字段名列表，字段名用逗号分割，最多四个字段能够被指定为主键
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // tcaplusservice.tcaplus_index 选项指定 Tcaplus 索引
    // 每个索引所包含的索引键必须是主键，并且所有索引字段集合的交集不能为空
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    //option(tcaplusservice.tcaplus_sharding_key) = "uin"; 用户可以自己显式设置分片字段，如果用户不显式设置，系统将默认采用主键字段为分片字段

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // 使用默认的 DefaultAesCipherSuite 加密函数，非必须设置选项
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // 设置加密密码字符串的 md5 值，非必须设置选项

    // 以下是表的字段定义
    // Tcaplus 表支持以下的数据类型：
    // 非嵌套类型：int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, bytes
    // 嵌套类型：message

    // 主键字段 (最多4个)
    int64 uin = 1;  // 主键字段必须是非嵌套类型
    string name = 2[(tcaplusservice.tcaplus_crypto) = true]; //message中string和bytes类型的字段可以指定为加密字段，非必须设置选项
    int32 region = 3;
    // 一张表最多只能包含4个主键字段

    // 普通值字段
    int32 gamesvrid = 4;
    int32 logintime = 5;
    int64 lockid = 6;
    bool is_available = 7;
    pay_info pay = 8; // 值字段的类型可以是自定义的结构体类型
}

message pay_info { // 使用 message 定义结构体

    int64 pay_id = 1;
    uint64 total_money = 2;
    uint64 pay_times = 3;
    pay_auth_info auth = 4;

    message pay_auth_info { // 结构体类型支持嵌套定义
        string pay_keys = 1;
        int64 update_time = 2;
    }
}
```
