<template>
  <div>
    <div>mina: {{}} </div>
    <div></div>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  name: "IndexPage",
  created: function(){
    this.currentLern = this.learns[0]
  },
  data: function () {
    return {
      currentLern: null,
      learns: [{
        mina: 47,
        keyword_vn: "hình như",
        keyword_jp: "ようです",
        structure: ```
          thể thông thường + ようです。
          だ -> な、の
        ```,
        explain: ```
          suy đoán dựa trên thông tin nhận từ giác quan, mang tính chủ quan.
          どうも: không rõ là điều mình nói có thật hay ko.
        ```,
        example: [
          "人が大勢集まっていますね。事故のようですね。",
          "せきもでるし、頭もいたいです。どうも風邪をひいたようです。",
        ],
        note: ```
          ミラーさんはいそがしそうです。
          ミラーさんはいそがしいようです。
          soudesu -> ve be ngoai,
          youdesu -> suy doan.
        ```,
      }],
    };
  },
  methods: {},
};
</script>

<style scoped>
</style>