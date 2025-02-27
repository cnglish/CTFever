<template>
  <PrimaryContainer>
    <form class="primary-form">
      <InteractiveBlock>
        <PrimaryArea :label="$t('common.text_input').toString()" v-model="input" id="input"/>
      </InteractiveBlock>
      <InteractiveDoubleColumns>
        <template v-slot:left>
          <PrimaryInput id="offset" :label="$t('common.text_offset').toString()" v-model="offset" type="number" min="1"
                        max="26"/>
        </template>
        <template v-slot:right>
          <PrimarySelector id="mode" :label="$t('common.text_mode').toString()" v-model="mode" :options="modeOptions"/>
        </template>
      </InteractiveDoubleColumns>
      <InteractiveBlock class="flex items-center justify-between">
        <div class="space-x-1">
          <PrimaryButton type="button" @click="exec">{{ $t('common.btn_execute').toString() }}</PrimaryButton>
        </div>
        <PrimaryButton type="button" danger @click="input = ''; output = '';">
          {{ $t('common.btn_clean').toString() }}
        </PrimaryButton>
      </InteractiveBlock>
      <InteractiveBlock>
        <PrimaryArea :label="$t('common.text_output').toString()" v-model="output" id="output" copyable/>
      </InteractiveBlock>
    </form>
    <PrimaryIntroduction title="凯撒密码" path="intro/ceasar-cipher" :references="references"/>
  </PrimaryContainer>
</template>

<script>
import PrimaryContainer from "~/components/tool/PrimaryContainer";
import InteractiveBlock from "~/components/tool/InteractiveBlock";
import PrimaryInput from "~/components/form/PrimaryInput";
import PrimaryArea from "~/components/form/PrimaryTextArea";
import InteractiveDoubleColumns from "~/components/tool/InteractiveDoubleColumns";
import PrimarySelector from "~/components/form/PrimarySelector";
import PrimaryButton from "~/components/form/PrimaryButton";

import ceasarCipher from '~/libs/ceasarCipher';
import PrimaryIntroduction from "~/components/tool/PrimaryIntroduction";

export default {
  name: "caesar-cipher",
  components: {
    PrimaryIntroduction,
    PrimaryButton,
    PrimarySelector,
    InteractiveDoubleColumns,
    PrimaryArea,
    PrimaryInput,
    InteractiveBlock,
    PrimaryContainer
  },
  head() {
    return {
      title: this.$t("tool.caesarCipher.title") + " - " + this.$t("app.name")
    };
  },
  data() {
    return {
      input: "",
      output: "",
      offset: 3,
      mode: "encode",
      modeOptions: [
        {
          label: "common.text_encode",
          value: "encode"
        },
        {
          label: "common.text_decode",
          value: "decode"
        }
      ],
      references: [
        {
          name: "Wikipedia: 凯撒密码",
          url: "https://zh.wikipedia.org/wiki/%E5%87%AF%E6%92%92%E5%AF%86%E7%A0%81"
        }
      ]
    }
  },
  methods: {
    exec() {
      this.output = this.mode === "encode" ? ceasarCipher.encode(this.input, this.offset) : ceasarCipher.decode(this.input, this.offset);
    }
  },
  watch: {
    offset: {
      handler(val) {
        this.$nextTick(() => {
          if (val < 1) {
            this.$data.offset = 1;
          }
          if (val > 25) {
            this.$data.offset = 25;
          }
        });
      }
    }
  }
}
</script>

<style scoped>

</style>
