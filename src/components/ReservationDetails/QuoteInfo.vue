<template>
  <q-card class="my-card" flat>
    <q-card-section class="row justify-between">
      <div class="row">
        <div class="text-dark q-mr-md" style="font-size: 16px;">
          {{ item.status }}
        </div>
      </div>
    </q-card-section>
    <q-separator inset />
    <q-card-section class="row">
      <div class="q-mr-sm">
        <q-img
          src="https://placeimg.com/500/300/nature"
          width="70px"
          height="93px"
        />
      </div>
      <div class="col q-px-sm">
        <div class="name" style="font-size: 14px;">{{ item.name }}</div>
        <div class="address ellipsis" style="font-size: 14px;">
          {{ item.address }}
        </div>
        <div class="option row">
          <div
            flat
            class="row"
            v-for="(option, index) in item.options"
            :key="index"
          >
            <q-btn
              flat
              style="color: #888888;"
              padding="0"
              size="14px"
              :label="option"
            />
            <q-separator class="q-mx-sm" vertical inset />
          </div>
        </div>
        <div
          class="row items-center text-secondary q-pt-md"
          style="font-size: 12px;"
        >
          {{ item.date }}
        </div>
      </div>
    </q-card-section>
    <q-card-section class="q-pt-none">
      <div v-if="item.status == '견적신청'">
        <q-btn
          :rounded="false"
          class="full-width"
          style="color: #151515; border: 1px solid #E4E4E4"
          label="취소하기"
          unelevated
        />
      </div>
    </q-card-section>
    <q-separator inset />
    <q-card-section
      class="costs-container row justify-between"
      v-if="item.costs"
    >
      <div>총 견적비용</div>
      <div style="color: #FF4848;">
        <span style="font-size:20px;">{{ item.costs }}</span> 원
      </div>
    </q-card-section>
  </q-card>
</template>

<script>
export default {
  data() {
    return {
      item: {
        status: "견적신청",
        date: "2020.07.01",
        name: "전국불도저",
        address: "경기도 화성시 괘랑4길 16-38번지 솔가타...",
        options: ["주거공간", "30평", "전체철거"],
        costs: "",
      },
    };
  },
};
</script>

<style scoped></style>
