<template>
  <PrimaryContainer>
    <form class="primary-form">
      <InteractiveBlock>
        <PrimarySelector v-model="method" :options="options"
                         :label="$t('common.text_type').toString()"></PrimarySelector>
      </InteractiveBlock>
      <InteractiveBlock>
        <PrimaryArea id="input" v-model="input" :label="$t('common.text_decoded').toString()" :rows="10"
                     copyable></PrimaryArea>
      </InteractiveBlock>
      <InteractiveBlock class="flex items-center justify-between">
        <div class="space-x-1">
          <PrimaryButton type="button" @click="encode">{{ $t('common.btn_encode') }} ↓</PrimaryButton>
          <PrimaryButton type="button" @click="decode">{{ $t('common.btn_decode') }} ↑</PrimaryButton>
        </div>
        <PrimaryButton type="button" danger @click="input = ''; output = '';">{{
            $t('common.btn_clean')
          }}
        </PrimaryButton>
      </InteractiveBlock>
      <InteractiveBlock>
        <PrimaryArea id="output" v-model="output" :label="$t('common.text_encoded').toString()"
                     :rows="10" copyable></PrimaryArea>
      </InteractiveBlock>
    </form>
  </PrimaryContainer>
</template>

<script>
import PrimaryContainer from "~/components/tool/PrimaryContainer";
import InteractiveBlock from "~/components/tool/InteractiveBlock";
import PrimaryButton from "~/components/form/PrimaryButton";
import PrimaryArea from "~/components/form/PrimaryTextArea";
import InteractiveDoubleColumns from "~/components/tool/InteractiveDoubleColumns";
import PrimarySelector from "~/components/form/PrimarySelector";

import * as base64 from "hi-base64";
import * as base32 from "hi-base32";

export default {
  name: "base-series",
  components: {
    PrimarySelector,
    InteractiveDoubleColumns,
    PrimaryArea,
    PrimaryButton,
    InteractiveBlock,
    PrimaryContainer
  },
  head() {
    return {
      title: this.$t("tool.baseSeries.title") + " - " + this.$t("app.name")
    };
  },
  methods: {
    encode() {
      this.output = this.method === "base64" ? base64.encode(this.input) : base32.encode(this.input);
    },
    decode() {
      this.input = this.method === "base64" ? base64.decode(this.output) : base32.decode(this.output);
    }
  },
  data() {
    return {
      input: "",
      output: "",
      method: "base64",
      options: [
        {
          label: "Base64",
          value: "base64"
        },
        {
          label: "Base32",
          value: "base32"
        }
      ]
    };
  },
}
</script>

<style scoped>

</style>
