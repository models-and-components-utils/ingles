<template>
  <div id="app">
    <div>
      <input type="text" v-model="text" @keyup.enter="encode">
    </div>
    <div>
      <audio v-if="show" controls>
        <source :src="encoded" type="audio/mp3">
        Your browser does not support the audio element.
      </audio>
    </div>
    <div>
      <textarea id="story" name="story"
        v-model="textArea" ref="inputkk" rows="5" cols="33" />
    </div>
  </div>
</template>

<script>
import { Base64 } from 'js-base64'
export default {
  name: 'app',
  components: {},
  watch: {
    encoded (value) {
      if (!value) {
        this.show = false
      }
    }
  },
  data: () => ({
    text: '',
    encoded: '',
    textArea: '',
    show: false
  }),
  methods: {
    encode () {
      this.textArea = ''
      this.$refs['inputkk'].select()
      document.execCommand('copy')
      // eslint-disable-next-line no-debugger
      this.show = !this.show
      let createTitle = this.text.split(' ')
      createTitle.forEach((value) => {
        this.textArea += `<span title="">${value}</span> \n\n`
      })
      this.encoded = `https://voice2.reverso.net/RestPronunciation.svc/v1/output=json/GetVoiceStream/voiceName=Heather22k?inputText=${Base64.encode(this.text)}&export=download`
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
