### velocity注意事项 (jira version:7.2)
#### 1. 获取访问的根路径：

``` ${req.getContextPath()} ```

#### 2. jquery
jira封装了jquery，使用AJS即可，方法如下：

``` javascript
AJS.$(document).ready(function() {
    #set($D = '$')
    //无法直接使用AJS.$.post
    AJS.${D}.post("${req.getContextPath()}/plugins/servlet/emtcserver",function(data){
        //TODO
    });
});
```

#### 3. select2
jira的aui含有select2，可以直接使用，需要注意的是select2的版本为3.5，查看[select2教程](http://select2.github.io/select2/)

> 示例：远程ajax获取数据

html部分：

*当select2使用ajax时，标签`<select></select>`不可用*
``` HTML
<!--
如果用于custom field，
当type="hidden",在issue的view页面，该字段无法编辑
当type="text",则字段可不编辑
 -->
<input type="hidden" name="$customField.id" id="$customField.id" class="select equipment" value="$!value"/>
```
javascript部分：
``` javascript
AJS.$(".equipment").auiSelect2({
    placeholder:"请选择",
    ajax:{
        quietMillis   : 1000,
        url     : "${req.getContextPath()}/plugins/servlet/emtcserver",
        dataType : 'json',
        type    : "post",
        data    : function(param,page){
            return {
                method : "equipmentList",
                search  : param,
                orderid : AJS.$("input.orderid").val() ,
            }
        },
        results : function(data,params){
            return {results:data};
        }
    },
    initSelection: function (element, callback) {
        //设置默认值
        var id = AJS.$(element).val();
        if(id){
            callback({ id: id, text: id });
        }
    }
});
```

#### 4. 加载资源（js、css）

* atlassian-plugin.xml

``` XML
<web-resource key="jira-resources" name="jira Web Resources">
    <dependency>com.atlassian.auiplugin:ajs</dependency>
    <resource type="download" name="jira.css" location="/css/jira.css"/>
    <resource type="download" name="jira.js" location="/js/jira.js"/>
    <resource type="download" name="select2.js" location="/js/select2.js"/>
    <resource type="download" name="images/" location="/images"/>
    <context>jira</context>
  </web-resource>
```

* vm页面加载资源

``` html
<link href="${req.getContextPath()}/download/resources/com.pactera.emtc.jira:jira-resources/jira.js" rel="stylesheet">
<script src="${req.getContextPath()}/download/resources/com.pactera.emtc.jira:jira-resources/jira.js"></script>
```
