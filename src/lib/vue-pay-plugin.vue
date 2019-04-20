<template>
  <div id="pay">
    <div :class="payOptions.isShow ? 'pay-container pay-container-active' : 'pay-container'">
      <div class="pay-info-panel">
        <div class="pay-info-header">
          <div class="close-pay-btn">
            <img src="../assets/icon-close-pay.png" alt="">
          </div>
          <div class="avatar">
            <img src="../assets/avatar.jpg" alt="">
          </div>
          <div class="tips">请输入支付密码</div>
        </div>
        <div class="pay-info-body">
          <div class="pay-info">
            <div class="seller-name">当当网</div>
            <div class="money">
              ¥<span>49.50</span>
            </div>
          </div>
          <div class="pay-type">
            <img src="../assets/icon-money.png" alt="">
            <span>零钱</span>
          </div>
          <!--密码-->
          <div class="pay-password-panel">
            <div class="pay-password-wrapper">
              <div class="pay-input" v-for="(item, index) in pwdLength" :key="index">
                <input type="password"  disabled>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!--下拉-->
      <div class="pay-keyboard-panel">
        <div class="pay-pulldown">
          <img src="../assets/icon-pulldown.png" alt="">
        </div>
        <!--键盘-->
        <div class="pay-keyboard-body">
          <!--1-9-->
          <div class="pay-keyboard">
            <div class="pay-key-wrapper" v-for="(item, index) in keyBoards" :key="item">
              <div class="pay-key">
                {{item}}
              </div>
            </div>
          </div>
          <!--0和删除部分-->
          <div class="pay-keyboard-bottom">
            <div class="pay-key-bottom pay-key-blank"></div>
            <div class="pay-key-bottom pay-key-wrapper">
              <div class="pay-key">0</div>
            </div>
            <div class="pay-key-bottom pay-key-blank">
              <img src="../assets/icon-delete.png" alt="" class="pay-key-delete">
            </div>
          </div>
        </div>
      </div>
    </div>
    <!--遮罩层-->
    <div class="mask" v-show="payOptions.isShow"></div>
  </div>
</template>

<script>
  export default {
    name: 'vue-pay-panel',
    props:['payOptions'],
    data () {
      return {
        //密码长度
        pwdLength:6,
        //键盘数字
        keyBoards:['1','2','3','4','5','6','7','8','9']
      }
    }
  }
</script>

<style>
  #pay{
    height:100%;
  }
  img{
    width:40px;
    vertical-align: middle;
  }
  .mask{
    position: fixed;
    top:0;
    left:0;
    right:0;
    bottom:0;
    background-color:rgba(0,0,0,.5);
    z-index:9;
  }
  /*画板下拉上升动画*/
  .pay-container{
    position:fixed;
    left:0;
    right:0;
    height:100%;
    bottom:-100%;
    z-index:99;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    overflow: hidden;
    transition: transform .2s;
    transform: translateY(0);
  }
  .pay-container-active{
    transition: transform .2s;
    transform: translateY(-100%);
  }
  /*支付信息显示部分*/
  .pay-info-panel{
    width:90%;
    margin:0 auto;
    background:#fff;
  }
  .pay-info-panel .pay-info-header{
    display: flex;
    align-items: center;
    padding:10px;
    border-bottom:1px solid #8BE898;
  }
  .pay-info-panel .close-pay-btn img{
    width:14px;
  }
  .pay-info-panel .avatar{
    border-radius: 5px;
    overflow: hidden;
    margin:0 10px;
  }
  .pay-info-panel .pay-info-body{
    width:90%;
    margin:0 auto;
    padding-bottom:20px;
  }
  .pay-info-panel .pay-info{
    border-bottom:1px solid #ccc;
  }
  .pay-info-panel .pay-info .seller-name{
    line-height:40px;
  }
  .pay-info-panel .pay-info .money{
    font-size:28px;
    font-weight:600;
    padding-bottom:10px;
  }
  .pay-info-panel .pay-info .money span{
    font-size:36px;
    vertical-align: top;
    margin-left:5px;
  }
  .pay-info-panel .pay-type{
    text-align: left;
    padding:10px 0;
  }
  .pay-keyboard-panel{
    height:310px;
  }
  /*下拉框部分*/
  .pay-pulldown{
    display: flex;
    justify-content: center;
    align-items: center;
    height:40px;
    background:#f6f6f6;
    border-bottom:1px solid #ccc;
    margin-top:50px;
  }
  .pay-pulldown img{
    width:36px;
  }
  /*密码框部分*/
  .pay-password-wrapper{
    display: flex;
    border-left:1px solid #ccc;
  }
  .pay-input{
    height:50px;
    box-sizing: border-box;
    border-top:1px solid #ccc;
    border-right:1px solid #ccc;
    border-bottom:1px solid #ccc;
  }
  .pay-input input{
    width:100%;
    height:100%;
    font-size:30px;
    text-align: center;
    background: none;
    outline: none;
    border:none;
  }
  /*键盘部分css*/
  .pay-keyboard-body{
    border-left:1px solid #ccc;
    height:220px;
  }
  .pay-keyboard{
    position: relative;
    display: flex;
    flex-wrap: wrap;
  }
  .pay-key-wrapper{
    background:#f6f6f6;
    width:33.3%;
    height:55px;
    box-sizing: border-box;
    border-right:1px solid #ccc;
    border-bottom:1px solid #ccc;
  }
  .pay-key{
    font-size:26px;
    text-align: center;
    line-height: 53px;
    width:100%;
  }
  /*键盘最底下的部分*/
  .pay-keyboard-bottom{
    display: flex;
  }
  .pay-key-bottom{
    width:33.3%;
    display: flex;
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
    border-right:1px solid #ccc;
    border-bottom:1px solid #ccc;
  }
  .pay-key-blank{
    background-color: #eee;
  }
  .pay-key-delete{
    width:40px;
  }
  /*加载动画*/
  .loading{
    padding:100px;
  }
  .loading div{
    padding-top: 100px;
  }
  .loading svg{
    -webkit-animation: loader 2s ease-in-out infinite alternate;
    animation: loader 2s ease-in-out infinite alternate;
  }
  @keyframes loader {
    from{transform: rotate(0deg);}
    to{transform: rotate(720deg);}
  }
  /*防止长按选择文本*/
  *{
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }
</style>
