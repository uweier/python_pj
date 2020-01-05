# 世界抑郁症情况及其相关因素研究

（图片加载较慢，若网络不佳请多刷新，感谢~）

使用Python 搭建Flask网站

请点击查看主要功能：
- [首页点击按钮跳转页面](https://github.com/uweier/python_pj/blob/master/image/shouye.png)
- [输入文本框筛选国家](https://github.com/uweier/python_pj/blob/master/image/number.png)
    - [输出的结果](https://github.com/uweier/python_pj/blob/master/image/number_result.png)
- [下拉列表筛选国家](https://github.com/uweier/python_pj/blob/master/image/gongzuo.png)
    - [输出的结果](https://github.com/uweier/python_pj/blob/master/image/gongzuo_result.png)

## 【10%】 github文档（templates、static、app.py、数据文档）
- [templates]()
- [static]()
- [app.py]()
- [data]()

## 【20%】 技术文档书写
### HTML档描述 30%
- 所有的HTML文件放置在templates文件夹中，其中base.html为基模板，其余html皆继承该基模板。
- base.html
    - 基本flask html模版档
    - 设定样式 href="static/hf.css"
- entry.html
    - flask html模版档，用户输入页使用 def index() 'html': #使用了 entry.html
- summary.html
    - 用户输出结果页使用 def yi_yu_select_9() -> 'html': #使用了 summary.html
- viewlog.html
    - 用户输出结果页使用 def view_the_log() -> 'html': #使用了 viewlog.html
    - viewlog.html对应系统日志。
- world_education.html
    - 用户输入/输出结果页使用 def yi_yu_select_5() -> 'html':#使用了 world_education.html
    - world_education_result.html
      - 用户输出结果页使用 def yi_yu_select_6() -> 'html':#使用了 world_education_result.html
- world_gdp.html
    - 用户输出结果页使用 def yi_yu_select_8() -> 'html':#使用了 world_gdp.html
- world_give_birth.html
    - 用户输出结果页使用 def yi_yu_select_7() -> 'html':#使用了 world_give_birth.html
- world_hbl.html
    - 用户输入/输出结果页使用 def yi_yu_select_2() -> 'html':#使用了 world_hbl.html
    - world_hbl_result.html
      - 用户输出结果页使用 def do_search_1() -> 'html':#使用了 world_hbl_result.html
- world_man_woman.html
    - 用户输出结果页使用 def yi_yu_select_3() -> 'html':#使用了 world_man_woman.html
- world_number.html
    - 用户输入/输出结果页使用 def yi_yu_select_1() -> 'html':#使用了 world_number.html
    - world_number_result.html
      - 用户输出结果页使用 def do_search_0() -> 'html':#使用了 world_number_result.html
- world_unemployment.html
    - 用户输出结果页使用 def yi_yu_select_4() -> 'html':#使用了 world_unemployment.html

所有HTML文件如下图所示：

![HTML文件](https://github.com/uweier/python_pj/blob/master/image/html_ms.png)

### Python档描述 30%
[python档下载]()

**app.py为唯一app档，可双击执行或於命令行输入python app.py执行**

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
7. return render_template，将后端的值传到前端HTML中。

### Web App动作描述 40%
1. 后端伺服器启动：执行 app.py 启动后端伺服器，等待web请求。启动成功应出现：* Running on http://127.0.0.1:8004/ (Press CTRL+C to quit)
2. 前端浏览器web 请求：访问 http://127.0.0.1:8004/ 启动前端web 请求
3. 后端伺服器web 响应：app.py 中 执行 了@app.route('/') 下的 index()函数，产生《世界抑郁症情况及其相关因素研究》的HTML页面 
```
def index() -> 'html':
    data_str = df_z.to_html()
    title = '世界抑郁症情况及其相关因素研究'
    return render_template('entry.html',
                           the_title = title,
                           the_res = data_str,
                          )  
```
4.前端浏览器收到web 响应：出现HTML，有HTML5表单的输入 input 类型(type) 为"SUBMIT"，变数名称(name)为"the_region_selected_1"
5.前端浏览器web 请求：用户选取不同按键，点击后，则产生新的web 请求，按照form元素中定义的method='POST' action='/world_number'，以POST为方法，动作为/world_number的web 请求
6.后端服务器收到用户web 请求，匹配到@app.route('/world_number'', methods=['POST'])的函数 yi_yu_select_1()




- Python代码模块和HTML代码块遵循Flask Jinja2规则，模块继承render_template(xxx.html,附加参数(传值给Web xxx.html界面))
    - return ：
        1. 传递函数的结果
        2. 传递函数运行的过程


- 【前端页面】点击按钮“总人数”，即可跳转到【总人数页面】；【总人数页面】在“搜索框”输入地区名称，点击“确定”，页面即可跳转到【搜索结果页面】；【总人数页面】点击按钮“首页”，即可跳转到【前端首页】。
- 【总人数页面】中，点击“播放”按键，即可实现地图轮播功能。

- 【前端页面】点击“患者的学历/就业情况”，即可跳转到【受教育程度和就业状况页面】；【受教育程度和就业状况页面】中点击“下拉菜单”选择地区名称，点击“筛选”，即可跳转到【对应地区数据图和表格结果页面】；【受教育程度和就业状况页面】点击按钮“首页”，即可跳转到【前端首页】。


- 其他页面动作与以上相似。



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
数据的传输(中介变量)
HTML（界面 .html name=""） 和 Python（服务端 .py）
数据的传输
1.HTML ---->Python代码传递
(用户界面的交互行为（表单提交）)

FLASK的方法：eg: request.form['user_color']

2.Python ----> HTML (Python代码执行的结果
（1.指定传给哪个HTML文件eg:results）
2.传递数据(函数返回值))
(接口)

Jinja2方法 ： python函数返回值 render_template html：{{ the_color }}
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
