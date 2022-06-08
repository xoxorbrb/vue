<script setup>
import { reactive } from 'vue';

const user = reactive({
  username: {
    value: '',
    validation: false,
    errorMessage: [],
    label: "NAME",
    id: 'username',
    type: 'text',
    placeholder: '이름을 입력해주세요.'
  },
  userid: {
    value: '',
    validation: false,
    errorMessage: [],
    label: "ID",
    id: 'userid',
    type: 'text',
    placeholder: '아이디를 입력해주세요.'
  },
  password: {
    value: '',
    validation: false,
    errorMessage: [],
    label: "PASSWORD",
    id: 'password',
    type: 'password',
    placeholder: '비밀번호를 입력해주세요'
  },
  passwordConfirm: {
    value: '',
    validation: false,
    errorMessage: [],
    label: "PASSWORD CONFIRM",
    id: 'passwordConfirm',
    type: 'password',
    placeholder: '비밀번호 확인'
  }
})
const login = (user) => {
    console.log(user)
}
const errMessage = (key) => {
  switch(key) {
    case !user[key].value:
      user[key].errorMessage.push(`${key}입력해주세요`);
      break;
  }
}
</script>
<template>
  <div class='content-wrapper'>
    <div class='inner-wrapper'>
      <form action="get" class="input-form">
        <div class="input-wrapper" v-for="input in user" :key="input.key">
          <label :for="input.id">{{input.id}}</label>
          <input :type="input.type" :placeholder="input.placeholder" v-model="input.value" @blur="errMessage(input.id)">
            <div v-if="input.errorMessage">
                <div v-for="err, index in input.errorMessage" :key="index">
                    {{err}}
                </div>
            </div>
          </div>

          

        <div class="btn--basic" @click="login(user)">
          확인
        </div>
      </form>
    </div>
  </div>
</template>
<style lang='scss' scoped>
.content-wrapper{
  width: 100%;
  .inner-wrapper{
    .input-form{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      .input-wrapper{
        display: flex;
        flex-direction: column;
        align-items:flex-start;
        label{
          font-size: 0.75rem; //
          margin-bottom: 5px;
        }
        input{
          height: 1.5rem;
          border-radius: 8px;
        }
        &:not(:last-child){
          margin-bottom: 20px;
        }
      }
    }
    .btn--basic {
      width: 10%;
      height: 20px;
      background-color: rgb(4, 192, 45);
      padding: 8px 0px;
      border: none;

      font-size: 1rem;
      color: rgb(227, 219, 219);
    }
  }
}
</style>
