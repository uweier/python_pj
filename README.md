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
- 所有的HTML文件放置在templates文件夹中，其中base.html为基模板，其余html皆继承该基模板。
- viewlog.html对应系统日志。
- world_number.html和world_number_result.html分别对应世界抑郁症总人数页面和其筛选后的结果页面，以此类推，其余html文件皆对应各自的页面。

所有HTML文件如下图所示：
![HTML文件](https://github.com/uweier/python_pj/blob/master/image/html_ms.png)

### Python档描述 30%
[python档下载]()

1. 安装并导入pandas、pyecharts、cufflinks、plotly等第三方包
2. pandas读csv文件
3. pyecharts的模块画地图、条形图等，并将部分图以html文件的方式导出
4. 安装Flask环境，导入flask和render_template函数，创建Flask对象实例
5. 创建url和函数，用url修饰函数，呈现不同的HTML页面
    - route(url) url:endpoint
    - methods (GET、POST)
    - 视图函数 def
6. 根据不同页面的不同功能写函数。以下面代码为例，函数yi_yu_select_4()将html文件读入并赋值给plot_all_4，使用resquest.form将用户输入传到html中对应的name中。
```
@app.route('/world_unemployment',methods=['POST'])
def yi_yu_select_4() -> 'html':
    with open("患病率与失业率对比图.html", encoding="utf8", mode="r") as f4: 
        plot_all_4 = "".join(f4.readlines())
    the_region = request.form["the_region_selected_4"]
    print(the_region)
    title = '世界抑郁症情况及其相关因素研究'
    return render_template('world_unemployment.html',
                            the_plot_all_4 = plot_all_4,
                            the_title = title,)
```

### Web App动作描述 40%

## 【40%】 数据交互（数据复杂度（是否存在与合理））

### 是否含有复杂数据结构的循环（列表循环、字典循环、集合循环） （20%）

### 是否含有合适的数据结构嵌套（20%）

### 是否含有合适的推导式（20%）
pyecharts数据处理时：
```
# 推导式 处理x轴
x轴 = [int(x) for x in df0.columns.values[1:]]
x轴_zx = [str(x) for x in x轴]
```
交互代码的改写：
```
# 原来的代码：
#     if search in countries.keys():
#         contents = [countries[search]]
#     else:
#         contents = ['您搜索的结果不存在！！']

# 改为推导式：
    contents = [countries[search] if search in countries.keys() else '您搜索的结果不存在！！']
```

### 是否含有适当的条件判断（20%）

### python 文档与html文档的数据交互（20%）

```
@app.route('/world_education_result',methods=['POST'])
def yi_yu_select_6() -> 'html':
    the_region = request.form["the_region_selected_6"]
    print(the_region)
    
    dfs = df.query("地区 in ['{}']".format(the_region))

    data_str6 = dfs.to_html()
   
    fig = dfs.set_index('地区').T.iplot(kind="bar",  xTitle="地区/年份",yTitle="地区数据", title="地区数据", asFigure=True)
    py.offline.plot(fig, filename="学历就业结果.html",auto_open=False)
    with open("学历就业结果.html", encoding="utf8", mode="r") as f6:
        plot_all_6 = "".join(f6.readlines())

    title = '世界抑郁症情况及其相关因素研究'
    return render_template('world_education_result.html',
                            the_plot_all_6 = plot_all_6,
                            the_title = title,
                            the_res_6 = data_str6,)
```

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
