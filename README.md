# 世界抑郁症情况及其相关因素研究之python项目

（图片加载较慢，若网络不佳请多刷新，感谢~）

**使用Python 搭建Flask网站**

主要功能：
- [首页点击按钮跳转页面](http://huangyuhui.pythonanywhere.com/)
- 输入文本框筛选国家
- [日志](http://huangyuhui.pythonanywhere.com/viewlog)

页面：
- 首页
- 总人数地图页
- 患病率地图页
    - 结果跳转页
- 男性与女性人数页
- 失业率页
- 妇女生育孩子数页
- 世界人均GDP页
- 总结页

## github文档（templates、static、app.py、数据文档）
- [templates](https://github.com/uweier/python_pj/tree/master/templates)
- [static](https://github.com/uweier/python_pj/tree/master/static)
- [app.py](https://github.com/uweier/python_pj/blob/master/app.py)
- [data](https://github.com/uweier/python_pj/tree/master/data)

## 技术文档书写
### HTML档描述
- 所有的HTML文件放置在templates文件夹中，其中base.html为基模板，其余html皆继承该基模板。
- base.html
    - 基本flask html模版档
    - 设定样式 href="static/hf.css"
- entry.html
    - flask html模版档，用户输入页使用 def index() ->'html'#此为首页
- summary.html
    - 用户输出结果页使用 def yi_yu_select_9() -> 'html'#此为总结页
- viewlog.html
    - 用户输出结果页使用 def view_the_log() -> 'html'#此为日志页
    - viewlog.html对应系统日志。
- world_gdp.html
    - 用户输出结果页使用 def yi_yu_select_8() -> 'html'#此为世界人均GDP页
- world_give_birth.html
    - 用户输出结果页使用 def yi_yu_select_7() -> 'html'#此为妇女生育孩子数页
- world_hbl.html
    - 用户输入/输出结果页使用 def yi_yu_select_2() -> 'html':#此为患病率地图页
    - world_hbl_result.html
      - 用户输出结果页使用 def do_search_1() -> 'html'
- world_man_woman.html
    - 用户输出结果页使用 def yi_yu_select_3() -> 'html'#此为男性与女性人数页
- world_number.html
    - 用户输出结果页使用 def yi_yu_select_1() -> 'html'#此为总人数地图页
- world_unemployment.html
    - 用户输出结果页使用 def yi_yu_select_4() -> 'html'#此为失业率页

### Python档描述 30%
[python档下载](https://github.com/uweier/python_pj/blob/master/app.py)

**app.py为唯一app档，可双击执行或於命令行输入python app.py执行**

1. 安装并导入pandas、pyecharts等第三方包
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

### Web App动作描述 
1. 后端伺服器启动：执行 app.py 启动后端伺服器，等待web请求。启动成功应出现：* Running on http://127.0.0.1:8004/ (Press CTRL+C to quit)
2. 前端浏览器web 请求：访问 http://127.0.0.1:8004/ 启动前端web 请求
3. 后端伺服器web 响应：app.py 中 执行 了@app.route('/') 下的 index()函数，产生《世界抑郁症情况及其相关因素研究》的HTML页面 
4. 前端浏览器收到web 响应：出现HTML，有HTML5表单的输入 input 类型(type) 为"SUBMIT"，变数名称(name)分别为"the_region_selected_1"，"the_region_selected_2"，"the_region_selected_3"，"the_region_selected_4"，"the_region_selected_7"，"the_region_selected_8"，"the_region_selected_9"
5. 前端浏览器web 请求：用户选取不同按键，点击后，则产生新的web 请求。以第一个world_number为例，按照form元素中定义的method='POST' action='/world_number'，以POST为方法，动作为/world_number的web 请求
6. 后端服务器收到用户web 请求，匹配到@app.route('/world_number', methods=['POST'])的函数 yi_yu_select_1()
7. def yi_yu_select_1() 函数，只是将前面pyecharts输出的html档读入，并存入plot_all_1，然后把用户提交的数据，以flask 模块request.form['the_region_selected_1']取到Web 请求中,使用flask模块render_template 函数把world_number.html模版输出。其中the_plot_all_1的值，对应plot_all_1之值。
8. 前端浏览器收到web 响应：world_number.html中the_plot_all_1的值正确的产生的话，前端浏览器会收到正确响应，看到地图。



简单描述：
- 【首页】点击按钮“总人数”、“患病率”，“男性与女性患者人数”，“患病率与失业率对比”，“每个妇女生育孩子数”，“世界人均GDP情况”、“主题观点总结”，即可跳转到对应页面；在各个页面点击按钮“首页”，即可跳转到【首页】。
- 【前端页面】点击按钮“患病率”，即可跳转到【患病率页面】；【患病率页面】在“搜索框”输入地区名称，点击“确定”，页面即可跳转到【搜索结果页面】；【患病率页面】点击按钮“首页”，即可跳转到【前端首页】。
- 【患病率页面】中，点击“播放”按键，即可实现地图轮播功能。

## 数据交互

### 推导式与if……else……
pyecharts数据处理时：
```
# 推导式 处理x轴
x_z = [int(x) for x in df0.columns.values[1:]]
x_z_zx = [str(x) for x in x_z]
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

### python 文档与html文档的数据交互
在world_hbl.html页面中的筛选地区功能里，用户在前端通过输入地区名称，即search = request.form['place']，form表单提交数据的input(input_name)，后端执行代码，使用for循环与if……else……筛选数据，存入contents中，指定传给world_hbl_result.html，然后在前端展示内容。

## HTML界面
### 实现数据的python——>HTML页面交互
- 用户在前端html页面通过input name="the_region_selected_2"，提交表单数据
- 后端python代码执行，指定将动作传给world_hbl.html，然后传递参数，返回plot_all_2、titles、contents、title的值
- Jinja2方法用于返回 {{ the_plot_all_2 }} 在后端的值。

### 符合jinja2标准

以base.html为例，{{ the_title }}为Jinja指令，指示将在呈现之前提供的一个值，对应后端代码中的title。
```
<!doctype html>
<html lang="zh-CN" >
    <head>
        <title>{{ the_title }}</title>
        <link rel="stylesheet" href="static/hf.css" />
    </head>
    <body>
        {% block body %}

        {% endblock %}
    </body>
</html>
```
## pythonanywhere
[http://huangyuhui.pythonanywhere.com/](http://huangyuhui.pythonanywhere.com/)

## 加分项
### viewlog日志
[日志](http://huangyuhui.pythonanywhere.com/viewlog)

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
