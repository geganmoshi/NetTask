# NetTask
###### 基于安卓AsynTask,fastjson,okhttp3封装的自定义网络请求框架
###### 该框架支持全自动数据解析,顺序请求，同步请求
###### 使用方法：
###### 在全局application中初始化设置okHttpClient
```html
 okHttpClient = new OkHttpClient.Builder()
                .connectTimeout(5 * 1000, TimeUnit.MILLISECONDS)
                .readTimeout(10 * 1000, TimeUnit.MILLISECONDS)
                .writeTimeout(10 * 1000, TimeUnit.MILLISECONDS)
                .build();
```
###### 调用方法：
```html
Net_Task请求参数：context,请求类型(0 get,1 post),解析数据返回类型(0 object,1 list),请求参数hashmap,请求参数json,解析的bean class,是否需要解析
Net_Task回调参数：单个类，list，是否请求成功，返回消息，返回码
根据请求参数然后解析回调参数

Net_Task net_task = new Net_Task(getActivity(),0,1,"",null,null, YourBean.class,true);
//请求头
net_task.setHeader("Authorization", MyApplication.authorization);
net_task.setListener(new Net_Task.OnInteract() {
    @Override
    public void call_back(Object callback, List callback_lst, Boolean is_success, String msg,String code) {
        if (YourActivity.this.isDestroyed()){
            return;
        }
        if (is_success){
          
        }else {
         
        }
    }
});
//顺序执行
net_task.execute();

//同步执行MyApplication.exec为自定义线程池
exec = Executors.newCachedThreadPool();
net_task.executeOnExecutor(exec);
```

###### 本NetTask解析的返回数据格式为:
```html
{
  "code": 0,
  "data": {
   
  },
  "msg": "string"
}
```
###### 默认code 200 为成功，500为失败，可根据具体情况修改NetTask里相应code
