<template>
  <q-card flat>
    <q-card-section class="q-py-none">
      <div v-for="(option, i) in visitsOptions" :key="i">
        <q-btn
          flat
          class="options-text full-width"
          style="height: 64px;"
          @click="selectedOption = option"
        >
          <div class="full-width  notosanskr-regular text-left">
            <q-icon style="margin-right: 20px" v-if="selectedOption == option">
              <img src="~assets/request_estimate-icon/radio-btn-selected.png" />
            </q-icon>
            <q-icon style="margin-right: 20px" v-else>
              <img
                src="~assets/request_estimate-icon/radio-btn-unselected.png"
              />
            </q-icon>
            {{ option }}
          </div>
        </q-btn>
        <q-separator inset="" v-if="i == 0"></q-separator>
      </div>
    </q-card-section>
  </q-card>
</template>

<script>
export default {
  data() {
    return {
      visitsOptions: ["예", "아니오"],
      selectedOption: "예",
    };
  },
  watch: {
    selectedOption(v) {
      v === "예" ? this.$emit("visit", true) : this.$emit("visit", false);
    },
  },
  mounted() {
    this.$emit("visit", true);
  },
};
</script>

<style scoped>
.options-text {
  font-size: 16px;
  line-height: 24px;
  letter-spacing: -0.8px;
  color: #15161a;
}
</style>
