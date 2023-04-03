<template>
  <div class="main">
    <div class="left_box">
      <div>Not sure what to do here</div>
      <div>maybe your apiKey :-></div>
      <input type="text" v-model="apiKey" />
    </div>
    <div class="right_box h-full flex">
      <div class="contentBox overflow-hidden">
        <div class="item">
          {{ result }}
          <div v-show="loading" class="loading"></div>
        </div>
      </div>
      <div class="inputBox flex flex-col">
        <textarea
          type="text"
          style="width: 50%; height: 100px; margin-bottom: 20px"
          v-model="searchText"
        />
        <div class="button" @click="submit">submit</div>
      </div>
    </div>
  </div>
</template>

<script>
import { Configuration, OpenAIApi } from 'openai'
export default {
  name: 'myChat',
  props: {},
  data() {
    return {
      loading: false,
      searchText: '',
      result: '',
      apiKey: '',
    }
  },
  methods: {
    async submit() {
      if (!this.apiKey) {
        alert('need your apiKey :->')
        return
      }
      this.loading = true
      this.result = ''
      const configuration = new Configuration({
        organization: 'org-PU0TFPfa5fLmjbpN3hFpbm1Q',
        apiKey: this.apiKey,
      })
      const openai = new OpenAIApi(configuration)
      // const res = await openai.listEngines()
      try {
        const res = await openai.createCompletion({
          // text mode
          model: 'text-davinci-003',
          prompt: this.searchText,
          max_tokens: 2048,
          temperature: 0.2,
        })
        if (res.status == 200) {
          this.loading = false
          this.result = res.data.choices[0].text
          this.searchText = ''
        } else {
          this.loading = false
          alert('error!')
        }
      } catch {
        this.loading = false
        alert('error!')
      }
    },
  },
}
</script>

<style scoped lang="less">
.overflow-hidden {
  overflow: hidden;
}
.flex-col {
  flex-direction: column;
}
.flex-1 {
  flex: 1 1 0%;
}
.w-full {
  width: 100%;
}
.h-full {
  height: 100%;
}
.flex {
  display: flex;
}
.relative {
  position: relative;
}
.main {
  height: 100%;
  display: flex;
  .left_box {
    width: 300px;
    background: #202123;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  .right_box {
    flex: 1;
    background: #343641;
    position: relative;
    flex-direction: column;
    align-items: center;
    .contentBox {
      color: #fff;
      padding-top: 100px;
      width: 80%;
      .item {
        width: 100%;
        height: 500px;
        border-radius: 5px;
        background: #202123;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: auto;
        font-size: 16px;
        .loading {
          width: 50px;
          height: 50px;
          background-image: url('../assets/loading.gif');
          background-size: 100% 100%;
          background-repeat: no-repeat;
        }
      }
    }
    .inputBox {
      position: absolute;
      left: 0;
      bottom: 0;
      width: 100%;
      height: 200px;
      background-image: linear-gradient(
        180deg,
        rgba(53, 55, 64, 0),
        #353740 58.85%
      );
      align-items: center;
      font-size: 14px;
      .button {
        width: 100px;
        height: 50px;
        background: #202123;
        border-radius: 10px;
        line-height: 50px;
        color: #fff;

        cursor: pointer;
      }
    }
  }
}
</style>
