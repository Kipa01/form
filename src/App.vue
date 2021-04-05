<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  computed: {}
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400&display=swap');
@import '~vue-multiselect/dist/vue-multiselect.min.css';

*,
*::after,
*::before {
  box-sizing: border-box;
}

body {
  font-family: 'Roboto', sans-serif;
  color: #000;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: rgb(20, 240, 203);
  background: linear-gradient(0deg, rgba(20, 240, 203, 1) 0%, rgba(9, 121, 120, 0.4) 50%, rgba(0, 255, 184, 1) 100%);
}

#app {
  max-width: 500px;
  width: 100%;
}

.form {
  font-size: 16px;
  padding: 25px 30px 15px;
  border-radius: 4px;
  margin: 0px auto;
  background-color: #fff;
  box-shadow: 0 4px 6px 0 rgba(0, 0, 0, 0.3);
  > div {
    margin-bottom: 20px;
  }
  .form__title {
    font-size: 20px;
    font-weight: 700;
    text-align: center;
    margin-bottom: 10px;
    padding-bottom: 10px;
    border-bottom: 1px solid #94aab0;
  }
  .label {
    display: inline-block;
    color: #94aab0;
    margin-bottom: 5px;
    &--req {
      position: relative;
      &:after {
        content: '*';
        position: absolute;
        right: 0;
        top: 0;
        color: red;
        transform: translateX(100%);
      }
    }
  }
  .input {
    border-radius: 4px;
    border: 1px solid #94aab0;
    outline: none;
    display: block;
    &.invalid {
      border-color: tomato;
    }
    &[type='text'] {
      width: 100%;
      padding: 12px;
    }
    &[type='date'] {
      padding: 5px;
      font-size: 16px;
      font-family: 'Roboto';
      &.invalid {
        color: tomato;
      }
    }
    &[type='tel'] {
      &.invalid {
        color: tomato;
        &::placeholder {
          color: tomato;
        }
      }
    }
  }
  .phone__field {
    display: flex;
    align-items: center;
    position: relative;
    &-pre {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 27px;
      width: 27px;
      margin-right: 3px;
      font-size: 14px;
      background: #94aab0;
      color: #ffffff;
    }
    input {
      font-size: 14px;
      max-width: 113px;
      padding: 5px 0px 5px 5px;
    }
    small {
      position: absolute;
      top: 100%;
      left: 0;
    }
  }
  .gender__body {
    display: flex;
    align-items: center;
    input {
      display: inline;
      margin: 0px 0px 0px 0px;
    }
    label {
      padding-left: 5px;
    }
    div {
      & + div {
        margin-left: 15px;
      }
    }
  }
  .checkbox {
    display: flex;
  }
  .form__button {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 170px;
    height: 45px;
    border-radius: 20px;
    font-size: 14px;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: 700;
    color: #524f4e;
    background: white;
    margin: 0px auto;
    box-shadow: 0 8px 15px rgba(0, 0, 0, .1);
    outline: none;
    cursor: pointer;
    transition: .2s;
    @media (min-width: 991px) {
      &:hover {
        background: #2EE59D;
        box-shadow: 0 15px 20px rgba(46, 229, 157, .4);
        color: white;
        transform: translateY(-4px);
      }
    }
  }
  .multiselect {
    &.invalid {
      .multiselect__tags {
        border-color: tomato;
        color: tomato;
      }
    }
  }
  .multiselect__single {
    margin: 0px 0px 0px 0px;
  }
  .multiselect--active {
    height: 40px;
    .multiselect__input {
      padding: 0px 0px 0px 0px;
    }
    .multiselect__tags-wrap {
      display: none;
    }
  }
  .input-invalid-message {
    color: tomato;
  }
  .submit {
    &__message {
      display: flex;
      width: 100%;
      height: 50px;
      justify-content: center;
      align-items: center;
      border-radius: 4px;
      font-size: 16px;
      color: #000000;
      font-weight: 700;
    }
    &__ok {
      color: #ffffff;
      background: #2EE59D;
    }
    &__err {
      background: red;
    }
  }
}


</style>
