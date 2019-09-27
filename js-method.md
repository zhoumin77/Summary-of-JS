##几个比较简单又好用的效果

- 关闭弹窗后，1 天之内不会再弹出，用记录的 cookie 来实现

```
    $('.ecshop-htc .close-btn').click(function(){
        $('.ecshop-htc').hide();
        $.cookie('ecshop_popup', 'yes', { expires: 1, path: '/' });
    })

    $(window).load(function(){
        if($.cookie('ecshop_popup')=="yes"){
            $('.ecshop-htc').hide();
        }else{
            $('.ecshop-htc').show();
        }
    })
```

- 底部的通栏，缓缓关闭,

```html
<div class="footer-awords">
  <div class="footer-awords-box">
    <p>
      16年内为上百个行业、420万客户提供个性化服务<br />
      拨打<span>021-6078-2321</span>，了解80%大中型企业的共同选择
    </p>
    <a id="wap_qq_footer" href="javascript:;" class="online-qq">立即咨询</a>
    <div class="footer-awords-close">
      <img
        src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABUAAAAVBAMAAABbObilAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAASUExURZubm0dwTJubm5qampubm5qaml11WEAAAAAGdFJOU/8AiIHHov4bwHMAAABgSURBVAjXbY/BDcAgDAOtTtBkgrIB3YBuwP7T1HE+foAEnGxIHOw3es0NXI0JYGKIH1K2wesGhSF5kGXUQZZRu5iavGKKq/6Is5uIY+GLg27vvY7V976Wx3N6fp/L5v0B3dEP+Tbiq90AAAAASUVORK5CYII="
        alt="关闭按钮"
      />
    </div>
  </div>
</div>
```
