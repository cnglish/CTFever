<template>
  <PrimaryContainer>
    <form class="primary-form">
      <!-- TODO: 自定义长短号 -->
      <InteractiveBlock>
        <PrimaryArea id="morse" v-model="input" :label="$t('common.text_original_content').toString()"
                     :rows="10" copyable></PrimaryArea>
      </InteractiveBlock>
      <InteractiveBlock class="flex items-center justify-between">
        <div class="space-x-1">
          <PrimaryButton type="button" @click="encodeMorse">{{ $t('common.text_encode').toString() }} ↓</PrimaryButton>
          <PrimaryButton type="button" @click="decodeMorse">{{ $t('common.text_decode').toString() }} ↑</PrimaryButton>
        </div>
        <PrimaryButton type="button" danger @click="input = ''; output = '';">{{
            $t('common.btn_clean').toString()
          }}
        </PrimaryButton>
      </InteractiveBlock>
      <InteractiveBlock>
        <PrimaryArea id="output" v-model="output" :label="$t('common.text_result_content').toString()"
                     placeholder="Morse code" :rows="10" copyable></PrimaryArea>
      </InteractiveBlock>
    </form>
    <PrimaryIntroduction title="摩尔斯电码" path="intro/morse-code" :references="references"/>
  </PrimaryContainer>
</template>

<script>
import PrimaryContainer from "~/components/tool/PrimaryContainer";
import InteractiveBlock from "~/components/tool/InteractiveBlock";
import PrimaryArea from "~/components/form/PrimaryTextArea";
import PrimaryButton from "~/components/form/PrimaryButton";

import {decode, encode} from 'xmorse';
import PrimaryIntroduction from "~/components/tool/PrimaryIntroduction";

export default {
  name: "morse-code",
  components: {PrimaryIntroduction, PrimaryButton, PrimaryArea, InteractiveBlock, PrimaryContainer},
  head() {
    return {
      title: this.$t("tool.morseCode.title") + " - " + this.$t("app.name")
    };
  },
  data() {
    return {
      input: "",
      output: "",
      references: [
        {name: '百度百科: 摩尔斯电码', url: 'https://baike.baidu.com/item/%E6%91%A9%E5%B0%94%E6%96%AF%E7%94%B5%E7%A0%81'}
      ]
    };
  },
  methods: {
    encodeMorse() {
      this.output = encode(this.input);
    },
    decodeMorse() {
      this.input = decode(this.output);
    },
  }
}
</script>

<style scoped>

</style>
