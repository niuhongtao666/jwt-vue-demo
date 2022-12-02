<template>
  <div class="about">
    <h2>JWT demo</h2>
    <ul>
      <li v-for="(item,index) in list" :key="index">
        {{item}}
      </li>
    </ul>
    <br />
    <button @click="getAddress">获取收货地址</button>
  </div>
</template>



<script>
let that=this;
export default {
  name: "home",
  data() {
    return {
      msg: "this is about",
      list:[]
    };
  },
  methods: {
    getAddress() {

      // var sign=md5('uid=1&address_id=345+私钥');

      // 私钥=md5(用户密码)


      // http://localhost:3000/api/order?uid=1
    
      var token=localStorage.getItem('token');
      this.$http
        .get("/api/address?uid=1&address_id=345", {
          auth: {
            username: token,
            password: 'sign'
          }
        })
        .then(function(response) {
          console.log(response);
          that.list=response.data.result;
        })
        .catch(function(error) {
          console.log(error);
        });
    }
  }
};
</script>