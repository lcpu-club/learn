# Problem 2022/11/12

你需要使用 Golang 写一个 Web 服务。

## 功能

这个 Web 服务需要有如下功能：

1. 对所有直接 `GET` 访问根目录 `/` 的请求，需要返回一个 JSON，具备三个字段，其中 `author_id` 是您的学号（使用 `string`），`lcpu_dev_email` 是您在 `work.lcpu.dev` 注册使用的邮箱，`request_time` 是访问 Unix 时间戳（`time.Now().Unix()` 可以获取）；响应头中 `Server` 字段需设置为 `my-web/0.1.0`；
2. 对所有 `POST` 访问 `/put-data` 的请求（请求的 Body 会负载一个 JSON，形如：`[12, 4345, 31, 234, 3311]`），需要把负载的整形数组存储起来；
3. 对所有 `GET` 访问 `/get-data` 的请求，需要把之前存储的所有数据从小到大排序后用 JSON 输出。

## 要求

1. 请从 `LISTEN_ADDR` 环境变量读取需要监听的地址，否则，请退出程序；
2. 请从 `TEMP_FILE` 环境变量读取允许您使用的临时文件地址；
3. 执行的中途程序有可能被直接暂停；请做好数据持久化工作。

## 如何提交结果

请创建一个 Git Repository，里面包含一个 Go Module （Package 为 `main`），可以通过 `go build` 直接编译出可执行文件。

将您的代码 Push 到：`http://0.study-group-judger.lcpu.dev/您的学号` (将您的学号替换为您的学号，如：2200000000)；密码请在学习组获取。

待 Push 完成后，您可以通过命令：`curl "http://0.study-group-judger.lcpu.dev/get-result?id=您的学号"` 查看评测结果。

## 命令入门

```bash
# Initialize the project
git init
go mod init my_problem_solution
# Create source file
touch main.go
# Now edit your code and debug your program ...

# When you finish:
git add .
git commit -m "Finish my project"
git push --set-upstream http://0.study-group-judger.lcpu.dev/你的学号 main
# Input 你的学号 as username, get the password in Learning group
curl "http://0.study-group-judger.lcpu.dev/get-result?id=你的学号"
# The output should reflect the judge result
```

## 可能会用到的标准库

```Go
    "encoding/gob"
    "encoding/json"
    "io"
    "io/ioutil"
    "net/http"
    "os"
    "sort"
    "strconv"
    "sync"
    "time"
```

## 出题人注释

1. Golang 的 json.Marshal 在传入长度为 0 的 slice 时，获得的结果是 []byte("NULL")；但是我们预期的结果是 byte("[]")，所以这里需要特别处理一下；
2. 关于数据的“持久化”，指的是在每次接收到新数据后，及时地将其保存至硬盘等非易失性介质。对于这一过程，评测机通常会给予一个 50 ms 的宽限期。关于保存至哪里，我们通过环境变量传入了一个临时文件地址；您可以尝试使用其余地址，但是评测机将不会为您处理临时文件的回收；这一过程为避免竞争读写，通常需要加锁；但是目前我们评测时假定不会同时有两个请求到达您编写的服务。
3. 对于持久化存储的数据，可以考虑使用json或者gob存储在硬盘上；当然，你也可以使用csv或空格分隔等你自己定义的形式，都是可能的选择

## 可能有用的资料

1. HTTP Methods: [Mozilla开发者文档](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
2. 什么是JSON: [Mozilla开发者文档](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
3. （了解）什么叫线程争用？: [StackOverflow上的答案](https://stackoverflow.com/questions/1970345/what-is-thread-contention)