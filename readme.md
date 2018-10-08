# JsBridge 教程

### 某块开发

 1 引入JsBridge.dll 和Newtonsoft.Json.dll

 2 编写某块代码 例如 

···
using System.Windows.Forms;
using JsBridge;
using Newtonsoft.Json.Linq;
namespace Module
{
    [System.Runtime.InteropServices.ComVisible(true)]
    public class MyModule : Object, IJsCall
    {
        public void onInit()
        {
           
        }

        public void fun1(JObject args, CallBack callBack)
        {
            MessageBox.Show(args["msg"].ToString(),args.ContainsKey("title")? args["title"].ToString():"提示");
            callBack.send(args);
        }

        public void fun2(JObject args, CallBack callBack)
        {
            MessageBox.Show(args["msg"].ToString(), args.ContainsKey("title") ? args["title"].ToString() : "提示w");
            callBack.send(args);
        }


    }
 
}

··· 

3 生成dll文件

4  在使用此模块的软件中修改 *module.json* 增加模块信息

···

"MyModule":{"dll":'path/to/MyModule.dll',"class":"Module.MyModule","methods":"fun1,fun2"}
···
