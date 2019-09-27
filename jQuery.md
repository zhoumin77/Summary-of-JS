# JQuery 笔记

标签（空格分隔）： 未分类

---

咨询页面，AJAX 获取内容，添加到 ul 内，prepend，添加到 ul 元素第一个开始。append，从最后面一个 li 添加

```
    //热点标签
    getHotLabel: function () {
        $.get( config.baseUrl + '/news/classify.php', {action: 'label'}, (e) => {
            const data = e;
            console.log(e);
            const labelUl = $('.zx_index_right_label_content ul');
            for(let a = 0 , lg = data.length; a < lg ; a++ ){
                const html = `<li><a href="/zx_label?termId=${escape(data[a].name)}">${data[a].name}</a></li>`
                labelUl.prepend(html);
            }
        })
    },
```

给每个 li 标签，加上点击事件，切换 tab 效果

```
  tabClick: function () {
        const lis = $('.zx_index_left_new ul li')
        const that = this;
        for(var a = 0 , lg = lis.length ; a < lg ; a ++){
            lis[a].onclick = function(){
                $(this).siblings().removeClass("zx_index_left_new_li_active");
                $(this).addClass("zx_index_left_new_li_active");
                that.label = $(this).html();
                that.page = 1;
                const listUl = $('.zx_index_left_new_list ul');
                listUl.empty();
                listUl.append( `<div class="loadEffect">
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                </div>` )
                that.getArticle();
            }
        }
    },

```
