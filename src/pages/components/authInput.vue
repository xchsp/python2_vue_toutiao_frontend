<template>
    <input
      type="text"
      class="input"
      :class="{error:!isOk}"
      @keyup.enter="jump"
      @input="dataChange"
      @blur="showTips"
    />
</template>

<script>
    export default {
        // name: "authInput",
        props:['rule','err_message'],
        data(){
          return {
            isOk:true
          }
        },
        methods:{
          jump(){
            this.$emit('keyup')
          },
          showTips($event){
            if(!this.isOk)
            {
              this.$toast.fail(this.err_message)
              let inputvalue=$event.target.value
              console.log(inputvalue)
            }
          },
          dataChange($event){

            let inputvalue=$event.target.value
            if(inputvalue)
            {
              let regex = new RegExp(this.rule)
              this.isOk = regex.test(inputvalue)
              this.$emit('input',inputvalue)
            }
            else {
              this.isOk = true
            }
          }
        }
    }
</script>

<style lang="less" scoped>
.input {
  margin-bottom: 20/@vv;
  width: 100%;
  height: 38/@vv;
  padding: 20px;
  box-sizing: border-box;
  background-color: #fff;
  border: none;
  border-bottom: 1px solid #666;
  outline: none;
}
.error {
  border-color: red;
}
</style>
