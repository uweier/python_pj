# 世界抑郁症情况及其相关因素研究

使用Python 搭建Flask网站

请点击查看主要功能：
- [首页点击按钮跳转页面](https://github.com/uweier/python_pj/blob/master/image/shouye.png)
- [输入文本框筛选国家](https://github.com/uweier/python_pj/blob/master/image/number.png)[输出的结果](https://github.com/uweier/python_pj/blob/master/image/number_result.png)
- [下拉列表筛选国家](https://github.com/uweier/python_pj/blob/master/image/gongzuo.png)[输出的结果](https://github.com/uweier/python_pj/blob/master/image/gongzuo_result.png)
## 【10%】 github文档（templates、static、app.py、数据文档（下载））
- [templates]()
- [static]()
- [app.py]()
- [数据文档]()

## 【20%】 技术文档书写
### HTML档描述 30%

### Python档描述 30%

### Web App动作描述 40%

## 【40%】 数据交互（数据复杂度（是否存在与合理））

### 是否含有复杂数据结构的循环（列表循环、字典循环、集合循环） （20%）

### 是否含有合适的数据结构嵌套（20%）

### 是否含有合适的推导式（20%）

### 是否含有适当的条件判断（20%）

### python 文档与html文档的数据交互（20%）


## 【10%】 自定义函数与模块功能（是否存在与合理)

### 函数和模块符合python PEP8标准（50%）

### 功能具有可扩展和丰富性（50%）

## 【10%】 HTML界面

### 实现数据的python——>HTML页面交互（如果Python有数据循环、复杂的数据结构，请务必检查前端是否正确接收到同样的数据传递结果）（80%）

### 符合jinja2标准（20%）

## 【10%】上传pythonanywhere/提交域名完善的个人网站

## 【10%】 加分项
### viewlog日志
第一次查找“地区”

![第一次输入“地区”](https://github.com/uweier/python_pj/blob/master/image/viewlog1.png)

第一次输出的结果

![第一次输出的结果](https://github.com/uweier/python_pj/blob/master/image/viewlog2.png)

第二次查找“地区”

![第二次输入“地区”](https://github.com/uweier/python_pj/blob/master/image/viewlog3.png)

第二次输出的结果

![第二次输出的结果](https://github.com/uweier/python_pj/blob/master/image/viewlog4.png)

两次的日志记录

![两次日志记录](https://github.com/uweier/python_pj/blob/master/image/viewlog5.png)

<b>代码展示：</b>
- 定义函数
  
  将每个Web请求会记录到vsearch.log文件中。
```
def log_request(req:'flask_request',res:str) -> None:
    with open('vsearch.log','a') as log:
        print(req.form, req.remote_addr, req.user_agent, res,file=log,sep='|')
        # print(str(dir(req)),res,file=log)
```

![函数的使用](https://github.com/uweier/python_pj/blob/master/image/viewlog6.png)


- 将数据读入一个嵌套列表里
```
@app.route('/viewlog')
def view_the_log() -> 'html':
    contents=[]
    with open('vsearch.log') as log:
        for line in log:
            contents.append([])
            for item in line.split('|'):
                contents[-1].append(escape(item))
    titles = ('Form Data', 'Remote_addr', 'User_agent', 'Results')
    return render_template('viewlog.html',
                           the_title = 'View Log',
                           the_row_titles = titles,
                           the_data = contents,)
```
