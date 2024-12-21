# protobuf测试

## 序列化与反序列化
* **protobuf配置文件**
```protobuf
// test.proto
syntax = "proto3";      // 声明protobuf的版本

package fixbug;         // 声明了代码所在的包（对于C++来说就是namespace）

// 定义登录请求消息类型     name    pwd
message LoginRequest
{
    string name = 1;
    string pwd = 2;
}

// 定义登录响应消息类型
message LoginResponse
{
    int32 errcode = 1;
    string errmsg = 2;
    bool success = 3;
}
```

**在当前目录下生成protobuf:** `protobuf test.proto --cpp_out=./`

* **main.cpp测试代码**
```cpp
#include "test.pb.h"
#include <iostream>
using namespace std;
int main()
{
    // 封装了login请求对象的数据
    LoginRequest req;
    req.set_name("zhang san");
    req.set_pwd("123456");

    // 对象数据序列化 -> char*
    std::string send_str;
    if (req.SerializeToString(&send_str));
    {
        std::cout << send_str << std::endl;
    }

    // 从send_str反序列化一个login请求对象
    LoginRequest reqB;
     if (reqB.ParseFromString(send_str))
     {
        std::cout << reqB.name() << std::endl;
        std::cout << reqB.pwd() << std::endl;
     }


    return 0;
}
```




## protobuf列表的使用
* **protobuf配置文件**
```protobuf
syntax = "proto3";      // 声明protobuf的版本

package fixbug;         // 声明了代码所在的包（对于C++来说就是namespace）

message ResultCode
{
    int32 errcode = 1;
    bytes errmsg = 2;
}

// 数据  列表  映射表
// 定义登录请求消息类型     name    pwd
message LoginRequest
{
    //string name = 1;
    //string pwd = 2;
    bytes name = 1;
    bytes pwd = 2;
}

// 定义登录响应消息类型
message LoginResponse
{
    //string errmsg = 2;
    ResultCode result = 1;
    bool success = 2;
}

// 定义获取好友请求消息类型
message GetFriendListsRequest
{
    uint32 userid = 1;
}

// 返回用户姓名、年龄、性别
message User
{
    bytes name = 1;
    uint32 age = 2;
    enum Sex
    {
        MAN = 0;
        WOMAN = 1;
    }
    Sex sex = 3;
}

// 定义获取好友请求响应消息类型
message GetFriendListsResponse
{
    ResultCode result = 1;
    repeated User friend_list = 2;
}
```


* **main.cpp测试代码**
```cpp
#include "test.pb.h"
#include <iostream>
#include <string>
using namespace fixbug;

int main()
{
    // 列表的使用
    /*
    LoginResponse rsp;
    ResultCode* rc = rsp.mutable_result();
    rc->set_errcode(0);
    rc->set_errmsg("登录处理失败了");
    */

    GetFriendListsResponse rsp;
    ResultCode* rc = rsp.mutable_result();
    rc->set_errcode(0);

    User* user1 = rsp.add_friend_list();
    user1->set_name("zhang san");
    user1->set_age(20);
    user1->set_sex(User::MAN);

    User* user2 = rsp.add_friend_list();
    user2->set_name("li si");
    user2->set_age(20);
    user2->set_sex(User::MAN);

    std::cout << rsp.friend_list_size() << std::endl;

    return 0;
}

```
