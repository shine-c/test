### 1.什么是 select2
        Select2是一个基于jQuery的可自定义的选择框,
    支持搜索，标记，远程数据集，无限滚动和许多其他高
    度使用的选项。
### 2. select2 特性
    * 多语言支持(超过40种语言的搜索)
    * 支持 ajax 远程数据
    * 支持 多主题 (eg: Bootstrap 3, Flat UI, Metro UI )
    * 可拓展
    * 全面的浏览器支持
        * IE 8+
        * Chrome 8+
        * Firefox 10+
        * Safari 3+
        * Opera 10.6+
    * 支持动态选项创建
    
### 3. select2 用法

    //select2 引入
    <link type="text/css" rel="stylesheet" href="/css/select2.css">  
    <script type="text/javascript" src="/js/select2.full.min.js"></script>    
    <script type="text/javascript" src="/js/i18n/zh-CN.js"></script></span>  
    
    
     <select class="js-example-basic-multiple js-states form-control" multiple="multiple"> //multiple 复选
          <option value="one" selected >First</option> //选中
          <option value="two" disabled="disabled">Second (disabled)</option> //禁止选择
           option value="three">Third</option>
     </select>
    
    
    
    
    $("select").select2({
          allowClear: true, //清除选择项
          maximumSelectionLength ：2  //多值选择, 限制选择的数量
         language: "zh-CN",  //支持语言
         
         theme: 'bootstrap'  //主题
         
         //对于单一的选择，为了占位符值出现，你必须有一个空白<option> 作为你的第一选择 <select>控制。
         //这是因为浏览器默认情况下会尝试选择第一个选项。如果你的第一个选项是非空的，浏览器将显示这个而不是占位符。
         //对于多选，你不能有一个空的<option>
         placeholder: "....", //占位符
          
         //数据加载 
         var data = {
                      "results": [
                            //每个对象应包含，至少，一个id和text
                            {
                              "id": 1,
                              "text": "Option 1",
                              "selected": true //选中
                            },
                            {
                              "id": 2,
                              "text": "Option 2",
                              "disabled": true  //禁用
                            }
                      ],
                      "pagination": {
                        "more": true 
                      }
                    };
         data: data  //json 
         ajax: {
             url: "",
             dataType: 'json',
             delay: 250,  // ajax 延时 用户在触发AJAX请求之前完成搜索词的输入
             //请求参数
             data: function (params) {
                // Query parameters will be ?search=[term]&type=public
                return {
                     q: params.term, // search term
                     page: params.page
                };
             },
             //API返回的数据转换为Select2预期的格式
             processResults: function (data) {
                   return {
                     results: data.items
                   };
             }
         }
         
         //下拉
         templateResult: formatState   //下拉框模板
         loseOnSelect: false           //选择后强制下拉菜单保持打开状态
         dropdownParent: $('#myModal') //下拉框替代元素
         
         
         //动态创建 option
         tags: "true", 
         
         //搜索
         matcher: match //自定义搜索结果匹配
         minimumInputLength: 3       //最小搜索字词长度
         maximumInputLength: 20      //最大的搜索字词长度
         minimumResultsForSearch: 20 //搜索的结果集条数限制             
                
    });
    
### 4. select2 常用 Events
    
    * change               选择或删除选项时触发
    * change.select2       限定范围的版本 change
    * select2:closing      下拉菜单关闭之前触发
    * select2:close        关闭下拉菜单时触发
    * select2:opening      下拉菜单打开之前触发
    * select2:open         每当打开下拉菜单时触发
    * select2:selecting    在选择结果之前触发
    * select2:select       选择结果时触发
    * select2:unselecting  选择被删除之前触发
    * select2:unselect     选择被删除触发
    
    eg :
        //时间 监听
        $('#mySelect2').on('select2:select', function (e) {
          // Do something
        });
        
        //触发
        $('#mySelect2').trigger({
            type: 'select2:select',
            params: {
                data: data
            }
        });
        
        
### 5. select2 高级功能
    Adapters and Decorators
    
    
