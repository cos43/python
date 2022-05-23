## Questions

#### Q1 给一个数组,统计数组里面单词出现的频率,不区分大小写,忽略单词空格

Example:

```python
Input: strings = ['I','Love','you ','and',' you','love','me']
Output: {'i': 1, 'love': 2, 'you': 2, 'and': 1, 'me': 1}
```

Solution:

```python
def solution(strings):
    data = {}
    for string in strings:
        string = string.strip().lower()
        if string in data:
            data[string] += 1
        else:
            data[string] = 1
    return data
```



#### Q2 给一个txt文件,统计单词出现的频率,不区分大小写

Example:

`sentences.txt`

```javascript
He
went
back
to
the
video
to
see
what
had
been
recorded
and
was
shocked
at
what
he
saw
```

```python
Input: filename = "sentences.txt"
Output: {'he': 2, 'went': 1, 'back': 1, 'to': 2, 'the': 1, 'video': 1, 'see': 1, 'what': 2, 'had': 1, 'been': 1, 'recorded': 1, 'and': 1, 'was': 1, 'shocked': 1, 'at': 1, 'saw': 1}
```

Solution:

```python
def solution(filename):
    data = {}
    with open(filename, 'r') as f:
        for line in f.readlines():
            line = line.replace("\n", "").strip().lower()
            if line in data:
                data[line] += 1
            else:
                data[line] = 1
    return data
```

#### Q3 读取`input`目录下所有txt文件,统计单词出现的频率,不区分大小写

Example:

```python
/input
		/a.txt
		/b.txt
Input: dictionary = "/input"
Output: {'he': 2, 'went': 1, 'back': 1, 'to': 2, 'the': 1, 'video': 1, 'see': 1, 'what': 2, 'had': 1, 'been': 1, 'recorded': 1, 'and': 1, 'was': 1, 'shocked': 1, 'at': 1, 'saw': 1}
```

Solution:

```python
def solution(dictionary):
  	filenames=os.listdir(dictionary)
    data = {}
    for file in filenames:
        with open(file, 'r') as f:
            for line in f.readlines():
                line = line.replace("\n", '').strip()
                if line in data:
                    data[line] += 1
                else:
                    data[line] = 1
    return data
```

#### Q4 Flask

使用flask编写一个聊天软件

**Q4.1** 编写`service.py`，需要实现如下函数：

* `get_users() `获取所有用户信息
* `get_user(user_id)`获取单个用户信息
* `add_user(username)` 用户加入
* `get_message()` 用户可以获取所有消息
* `send_message(sender,receiver,content)` 实现一个接口，用户发送消息

**Q4.2** 编写一个测试文件`service_test.py`, 测试你写的`service.py`是否正确

**Q4.3** 编写`server.py`, 需要实现：

* 实现一个接口，admin可以获取所有用户信息
* 实现一个接口，admin获取单个用户信息
* 实现一个接口，用户可以注册
* 实现一个接口，用户可以获取所有消息
* 实现一个接口，用户发送消息

#### Q5 装饰器

**Q5.1** 创建add_log装饰器，被装饰的函数打印日志信息,如果`server`函数传递了port则输出port，如果没有传递则默认3000

```python
def add_log(function):
    def wrapper(*args, **kwargs):
        pass
    return wrapper
@add_log
def server(port):
    return f"Listening on http://localhost:"
```

Example:

```python
print(server('8080'))
#log: Listening on http://localhost:8080
print(server())
#log: Listening on http://localhost:3000
```

Solution:

```python
def add_log(function):
    def wrapper(*args, **kwargs):
        if len(args) > 0:
            return "log: " + function(*args) + args[0]
        else:
            return "log: " + function(*args) + '3000'
    return wrapper
```

**Q5.2** 创建set_port装饰器，要求可以修改被装饰函数的port

```python
def set_port(argument):
    def func_outer(function):
        def func_inner(*args):
            pass
        return func_inner
    return func_outer
  
def get_port_from_environment():
    return '4000'

@set_port("3000")
def server_1(port):
    return 'http://localhost:' + port


@set_port(get_port_from_environment)
def server_2(port):
    return 'http://localhost:' + port
```

Example:

```python
print(server_1())
#http://localhost:3000
print(server_2())
#http://localhost:4000
```

Solution:

```python
def set_port(argument):
    def func_outer(function):
        def func_inner(*args):
            if isinstance(argument, str):
                return function(argument, *args)
            else:
                return function(argument(), *args)
        return func_inner
    return func_outer
```




