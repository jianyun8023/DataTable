### DataTable  jq插件  的服务器端参数解析工具


##使用方式  

可以使用spring mvc  注解方式 或者 使用DataTableUtils 工具解析参数
 **使用spring mvc 注解方式需要 配置 注解的解析类** 


```xml
         <mvc:annotation-driven>
		<mvc:argument-resolvers>  
                    <bean class="cc.yihy.utils.DataTableResolver"/>  
                </mvc:argument-resolvers>  
		
	 </mvc:annotation-driven>
```


##简单使用示例

``` java
	/**
	 * 使用spring mvc  处理Datatable的参数   使用注解
	 * @param tableRequest  DataTable 请求参数
	 * @return
	 * @throws Exception
	 */
	@RequestMapping("list")
	public DataTableResponse<User> getData(@DataTableParam DataTableRequest tableRequest) throws Exception{
		
		//对请求参数解析，生成 排序条件、列搜索对象、全局搜索对象
		ResultObj<User> resultObj = tableRequest.getResultObj(User.class);
		//dataTable 相应参数   会被处理成json
		DataTableResponse<User>  user= new DataTableResponse<User>();
		
		return user;
	}
	
	@RequestMapping("list1")
	public DataTableResponse<User> getList(HttpServletRequest request) throws Exception{
		//不使用注解
		
		DataTableRequest param = DataTableUtils.getParam(request);
		
		//对请求参数解析，生成 排序条件、列搜索对象、全局搜索对象
		ResultObj<User> resultObj = param.getResultObj(User.class);
		//dataTable 相应参数   会被处理成json
		DataTableResponse<User>  user= new DataTableResponse<User>();
		
		return user;
	}
```

代码也比较简单 实现请看里面代码