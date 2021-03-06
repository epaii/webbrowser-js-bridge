# JsBridge 教程

## 模块开发

#### 1 引入JsBridge.dll 和Newtonsoft.Json.dll
#### 2 编写某块代码 例如 

```
using System.Windows.Forms;
using JsBridge;
using Newtonsoft.Json.Linq;
namespace Module
{
    [System.Runtime.InteropServices.ComVisible(true)]
    public class MyModule : Object, IJsCall
    {
        public void onInit(WebBrowser webBrowser, Form form)
        {
           
        }

        public void fun1(JObject args, CallBack callBack)
        {
            MessageBox.Show(args["msg"].ToString(),args.ContainsKey("title")? args["title"].ToString():"提示");
            callBack.success(args);
        }

        public void fun2(JObject args, CallBack callBack)
        {
            MessageBox.Show(args["msg"].ToString(), args.ContainsKey("title") ? args["title"].ToString() : "提示w");
            callBack.success(args);
        }
		
		 public void onDestroy()
        {
             
        }


    }
 
}

```

#### 3 生成dll文件

#### 4  在使用此模块的软件中修改 *module.json*（exe文件同级目录） 增加模块信息

```
"MyModule":{"dll":'path/to/MyModule.dll',"class":"Module.MyModule","methods":"fun1,fun2"}
```

#####  CallBack 类 方法

```
  callBack.success(data);//成功时候
  callBack.error(data);//失败时候
  callBack.callFunction(int.Parse(args["onOk"].ToString()), data);//参数中某一个函数
```







## 项目开发

#### 1 引入JsBridge.dll 和Newtonsoft.Json.dll
#### 2 创建webbrowser， 让webbrowser具有bridge功能的代码

```
 Bridge.bridgeWebBrowser(webbrowser, this);
```
#### 3 在exe所在目录下创建 module.json，并添加模块。 如：

```
{
"window":{"dll":'C:/Users/Administrator/source/repos/Module/bin/Debug/Module.dll',"class":"Module.Window","methods":"alert,alert2"}
}

```

#### 4 在html 代码中编写js 代码调用模块

```
   <script>
   
   JsBridgeReady = function()
   {
      JsBridge.require("window").alert2({msg:"提示内容","title":"消息"},function(data){
		alert(data.msg);
	  });
   }
   
   </script>
```

如果报JSON未定义，则需要在html中增加

```
 <meta http-equiv="X-UA-Compatible" content="IE=edge">
```


## 工具类WsLibs.Tools.Utils

```

Utils.getApplicationRootDir();//获取exe文件所在目录

Utils.gile_get_content(string path);

Utils.getConfig();//获取config.json 配置内容

Utils.getPathInConfig(string name) ;//获取配置中的路径，智能化


```
