<template>
<div>
  <a href="https://open.weixin.qq.com/connect/oauth2/authorize?appid=wx520c15f417810387&redirect_uri=https%3A%2F%2Fwxtest.stelo.io%2Fwechat_outh&response_type=code&scope=snsapi_base#wechat_redirect">请点击并完成授权</a>
  <h3 v-if="code">当前授权码为{{code}}</h3>
  <a v-on:click="rqserver(code)">点击此处完成服务端授权</a>
  <h3 v-if="response">当前授权结果为{{response}}</h3>
</div>
</template>

<script>
export default {
  data() {
    return {
      code: '',
      response: ''
    }
  },
  created() {
    var query = window.location.search.substring(1);
       var vars = query.split("&");
       for (var i=0;i<vars.length;i++) {
               var pair = vars[i].split("=");
               if(pair[0] == 'code'){
                 this.code = pair[1];
               }
       }
  },
  methods: {
    rqserver: function(code) {
      var xhr = new XMLHttpRequest();
      var self = this;
            xhr.open("GET", 'http://wxtest.stelo.io/usr/api/v1/code-auth?code='+code);
            xhr.onload = function() {
              self.response = xhr.responseText;
              console.log(xhr.responseText);
            };
            xhr.send();
    }
  },
}
</script>

<style>

</style>