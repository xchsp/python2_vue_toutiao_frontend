<template>
  <div class="container">
     <div class="closeBtn">
      <span @click="$router.back()" class="iconfont iconjiantou2"></span>
    </div>
    <div class="logo">
      <span class="iconfont iconnew"></span>
    </div>

    <div class="inputName">
        <authInput
          @input="setUserName"
          err_message="请输入正确的用户名(手机号)"
          placeholder="用户名/手机号"
          rule="^[1][3,4,5,7,8][0-9]{9}$"
        />
    </div>
      <div class="inputemail">
      <authInput
        @input="setemail"
        err_message="请输入正确的email"
        placeholder="昵称"
        rule="^([a-zA-Z0-9]+[_|\_|\.]?)*[a-zA-Z0-9]+@([a-zA-Z0-9]+[_|\_|\.]?)*[a-zA-Z0-9]+\.[a-zA-Z]{2,3}$"
      ></authInput>
    </div>
    <div class="inputPwd">
      <authInput
        @input="setPassword"
        err_message="请输入正确的密码3-10位"
        placeholder="请输入密码"
        rule="^\d{3,10}$"
        type="password"
      ></authInput>
    </div>
    <div class="btn">
        <authBtn text="注册" @clickxx="sendRegister"/>
    </div>
  </div>
</template>

<script>
    import authBtn from '@/pages/components/authBtn'
    import authInput from '@/pages/components/authInput'
    export default {
      data(){
        return {
            username:'',
            password:'',
            email:''
        }
      },
      components:{
        authBtn,
        authInput
      },
      methods:{
        setUserName(username){
          this.username = username
        },
        setemail(name) {
          this.email = name
        },
        setPassword(password) {
          this.password = password
        },
        sendRegister(){
          this.$axios({
            url:'/register',
            method: 'POST',
            data:{
              username:this.username,
              email:this.email,
              password:this.password,
            }
          }).then(res => {
            if(!res)
              return
            console.log('then:'+res.message)
            this.$toast.success(res.message)
          })

          console.log('sendRegister')
        }
      }
    }
</script>

<style lang="less" scoped>
.container {
  padding: 20/@vv;
}
.closeBtn {
  .iconfont {
    font-size: 27/@vv;
  }
}
.logo {
  display: flex;
  justify-content: center;
  .iconfont {
    color: #d81e06;
    font-size: 126/@vv;
  }
}
.btn {
  margin: 50px auto 0;
}
</style>
