<template>
  <div class="bg-grey-3" style="min-height:100vh;">
    <div class="bg-white">
      <router-link
        :to="{ name: 'my_account' }"
        style="
    text-decoration: none;"
      >
        <div class="account-info notosanskr-regular">
          <div class="user-greet">
            {{$store.getters.user.name}} 님 안녕하세요.
          </div>
          <q-icon class="text-dark" size="24px">
            <img src="~assets/arrow_right.svg" />
          </q-icon></div
      ></router-link>
      <div class="q-px-none">
        <q-separator color="grey-4" size="1px" />
      </div>
      <div class="row items-center justify-evenly">
        <q-item-section
          class="top-tabs column items-center"
          @click="alertNotReady"
        ><!--@click="$router.push({ name: 'interested_company' })"-->
          <q-img
            :src="require('src/assets/interested_companies.svg')"
            :ratio="1"
          />
        </q-item-section>

        <q-item-section
          class="top-tabs column items-center"
          @click="alertNotReady"
        ><!--@click="$router.push({ name: 'company_inquire' })"-->
          <q-img :src="require('src/assets/company_inquiry.svg')" :ratio="1" />
        </q-item-section>

        <q-item-section
          class="top-tabs column items-center"
          @click="alertNotReady"
        ><!--@click="$router.push({ name: 'work_schedule' })"-->
          <q-img :src="require('src/assets/work_schedule.svg')" :ratio="1" />
        </q-item-section>
      </div>
    </div>

    <div class="bg-white q-mt-sm q-pa-none ">
      <div class="my-location row items-center justify-between" @click="goAddress">
        <div class="col-8 notosanskr-regular">
          <p class="text-label q-ma-none notosanskr-medium">내 위치</p>
          <p class="address-text q-ma-none  notosanskr-regular">
            {{($store.getters.user.address1 || '주소를 입력해주세요') + ' '}}
            {{$store.getters.user.address2}}
          </p>
        </div>
        <q-icon class="text-dark" size="20px">
          <img src="~assets/arrow_right.svg" />
        </q-icon>
      </div>
      <div class="my-phone row items-center justify-between" @click="$router.push({ name: 'my_account' })">
        <div class="col  notosanskr-regular">
          <p class="q-ma-none text-grey notosanskr-medium">연락처</p>
          <p class="phone-number q-ma-none q-pt-sm notosanskr-bold"
             :style="{ 'opacity': $store.getters.user.phone ? 1: 0.5 }">
            {{$store.getters.user.phone || '핸드폰번호를 입력해주세요.' }}
          </p>
        </div>

<!--        <button class="verification-completed">-->
<!--          <q-icon name="done" class="text-dark" size="16px"></q-icon>-->
<!--          인증완료-->
<!--        </button>-->
      </div>
      <q-separator size="1px" />

<!--      <div class="notosanskr-medium">-->
<!--        <div class="recent-quote-heading">-->
<!--          최근견적-->
<!--        </div>-->
<!--        <q-separator size="3px" style="background: #151515" />-->
<!--        <div class="store-info">-->
<!--          <button class="store-name">전국불도저</button>-->
<!--          <button class="store-call">-->
<!--            <q-icon class="text-dark" size="24px">-->
<!--              <img src="~assets/store_call.svg" />-->
<!--            </q-icon>-->
<!--            070-345-0789-->
<!--          </button>-->

<!--          <q-card-->
<!--            class="my-card q-mt-md"-->
<!--            style="    padding: 20px;"-->
<!--            :bordered="false"-->
<!--          >-->
<!--            <q-card-section class="info-items row justify-between">-->
<!--              <div class="label-text col-3">주소</div>-->
<!--              <div class="info-text col-9">-->
<!--                경기도 치움시 철거4길 16-38번지 치움 타운하우스-->
<!--              </div>-->
<!--            </q-card-section>-->
<!--            <q-card-section class="info-items row justify-between">-->
<!--              <div class="label-text col-3">타입</div>-->
<!--              <div class="info-text col-9 row">-->
<!--                <div>-->
<!--                  주거공간-->
<!--                </div>-->
<!--                <q-separator size="2px" vertical style="margin: 0 6px;" />-->
<!--                <div>-->
<!--                  30평-->
<!--                </div>-->
<!--              </div>-->
<!--            </q-card-section>-->
<!--            <q-card-section class="info-items row justify-between">-->
<!--              <div class="label-text col-3">작업 유형</div>-->
<!--              <div class="info-text col-9">-->
<!--                폐기물-->
<!--              </div>-->
<!--            </q-card-section>-->
<!--            <q-card-section class="info-items row justify-between">-->
<!--              <div class="label-text col-3">작업 일시</div>-->
<!--              <div class="info-text col-9">-->
<!--                미정-->
<!--              </div>-->
<!--            </q-card-section>-->
<!--            <q-card-section class="info-items row justify-between">-->
<!--              <div class="label-text col-3">진행 상태</div>-->
<!--              <div class="info-text col-9 text-secondary">-->
<!--                견적신청-->
<!--              </div>-->
<!--            </q-card-section>-->
<!--          </q-card>-->
<!--        </div>-->
<!--      </div>-->
    </div>

    <div class="bg-white q-mt-md q-py-none">
      <q-list separator inset size="3px" class="notosanskr-medium">
        <q-item style="height: 60px;" clickable v-ripple @click="alertNotReady">
          <q-item-section class="list-item-routes">
            <div>
              공사 후기 작성
              <q-icon class="text-dark q-ml-sm" size="14px">
                <img src="~assets/new.svg" />
              </q-icon>
            </div>
          </q-item-section>
          <span class="material-icons" style="font-size: 26px;">
            keyboard_arrow_right
          </span>
        </q-item>
        <q-item style="height: 60px;" clickable v-ripple @click="alertNotReady">
          <q-item-section class="list-item-routes">
            철거˙폐기물 전문가로 가입
          </q-item-section>
          <span class="material-icons" style="font-size: 26px;">
            keyboard_arrow_right
          </span>
        </q-item>
        <q-item style="height: 60px;" clickable v-ripple @click="$router.push({ name: 'notice' })">
          <q-item-section class="list-item-routes">공지사항 </q-item-section>
          <span class="material-icons" style="font-size: 26px;"
            >keyboard_arrow_right</span>
        </q-item>
        <q-item style="height: 60px;" clickable v-ripple @click="alertNotReady">
          <q-item-section class="list-item-routes">설정 </q-item-section>
          <span class="material-icons" style="font-size: 26px;"
            >keyboard_arrow_right</span
          >
        </q-item>
        <q-item
          style="height: 60px;"
          clickable
          v-ripple
          @click="logout"
        ><!--@click="open('bottom')"-->
          <q-item-section class="list-item-routes" style="color: #767676;"
            >로그아웃
          </q-item-section>
          <span class="material-icons" style="font-size: 26px;"
            >keyboard_arrow_right</span
          >
        </q-item>
      </q-list>
    </div>

    <div class="bg-white q-mt-md q-py-none" @click="call">
      <div
        class="row justify-between notosanskr-medium"
        style="padding: 21px 16px;"
      >
        <div>
          <div>
            고객센터
            <span class="service-number q-pl-xs">1588-1234</span>
          </div>
          <div class="operating-hours">
            운영시간 / 주 5일 평일 11:00 ~ 18:00
          </div>
        </div>
        <q-icon class="text-dark q-ml-sm" size="42px">
          <img src="~assets/call_service.svg" />
        </q-icon>
      </div>
    </div>

    <div style="height: 110px"></div>
    <q-dialog v-model="dialog" :position="position">
      <q-card
        style="height: 241px;"
        :style="widthMax"
        class="popup-content notosanskr-medium"
      >
        <q-card-section class="row items-center no-wrap  q-py-none">
          <div class="text-right full-width" @click="dialog = false">
            <q-btn
              class="close-button"
              flat
              style="color: #151515"
              label="닫기"
            />
          </div>
        </q-card-section>

        <q-card-section
          class="row items-center no-wrap absolute-bottom q-pa-none"
        >
          <q-toolbar class="bg-white text-white q-py-none" :style="widthMax">
            <div class="popup-body full-width column items-center">
              <div class="header">폐기물 버리기!</div>
              <div class="sub-header">
                폐기물 작업을 진행하기 전 업체에게 견적 받는 방법을
                선택해주세요.
              </div>
              <button class=" bg-secondary">
                업체 한 곳 선정해서 견적받기
              </button>
            </div>
          </q-toolbar>
        </q-card-section>
      </q-card>
    </q-dialog>

    <!--  Dialog Not Ready  -->
    <q-dialog v-model="dialogNotReady">
      <q-card align="center">
        <q-card-section>
          <div class="text-h5">준비중인 페이지입니다.</div>
        </q-card-section>
        <q-card-section>
          고객님, 죄송합니다. 현재는 베타서비스(1월 ~ 3월) 기간이며, 4월 초로
          정식 런칭예정입니다.
        </q-card-section>
        <q-card-actions align="center">
          <q-btn label="확인" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
export default {
  name: 'MyPage',
  components: {},
  data () {
    return {
      dialog: false,
      position: 'bottom',
      dialogNotReady: false,
    }
  },
  computed: {
    widthMax () {
      return {
        width: window.innerWidth + 'px', 'max-width': '1000px'
      }
    }
  },
  methods: {
    open (position) {
      this.position = position
      this.dialog = true
    },

    goAddress () {
      this.$router.push({ name: 'address', query: { back: 'my_page' } })
    },

    call () {
      window.open('tel:01040840660')
    },

    logout () {
      this.$store.commit('logout')
      alert ('로그아웃 되었습니다.')
      this.$router.push({ name: 'home' })
    },

    alertNotReady () {
      this.dialogNotReady = true
    }
  },
  created () {
    this.$emit('changeHeadingName', '마이페이지')
  }
}
</script>

<style lang="scss" scoped>
.account-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 76px;
  padding: 0 16px;

  .user-greet {
    font-weight: 500;
    font-size: 22px;
    line-height: 36px;
    letter-spacing: -1.1px;
    color: #151515;
  }
}

.top-tabs {
  min-width: 114px;
  min-height: 110px;
  cursor: pointer;
}

.my-location {
  height: 118px;
  padding: 20px 16px;

  .text-label {
    font-size: 13px;
    line-height: 20px;
    letter-spacing: -0.65px;
    color: #767676;
  }

  .address-text {
    font-size: 16px;
    line-height: 24px;
    letter-spacing: -0.8px;
    color: #151515;
    margin-top: 10px;
  }
}

.my-phone {
  padding: 20px 16px;
  .phone-number {
    font-family: Roboto;
    font-size: 16px;
    line-height: 24px;
    color: #151515;
  }

  .verification-completed {
    background: white;
    padding: 4px 8px;
    border: 1px solid #cccccc;
    box-sizing: border-box;
    border-radius: 4px;
  }
}

.recent-quote-heading {
  padding: 41px 16px 15px;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: -0.8px;
  color: #151515;
}

.store-info {
  padding: 25px 16px 60px;

  button {
    border-radius: 100px;
    border: none;
    font-weight: 500;
    font-size: 13px;
    line-height: 28px;
    text-align: center;
    letter-spacing: -0.65px;
    color: #ffffff;

    &.store-name {
      background: #2cb3ff;
      margin-right: 8px;
    }

    &.store-call {
      color: #151515;
      background: #f7f7f6;
      border: 1px solid #f0f0f0;
    }
  }

  .info-items {
    font-size: 13px;
    line-height: 20px;
    letter-spacing: -0.65px;
    padding: 0 0 15px;
    .label-text {
      color: #767676;
    }
    .info-text {
      color: #151515;
    }
  }
}

.list-item-routes {
  font-size: 15px;
  line-height: 22px;
  letter-spacing: -0.75px;
  color: #151515;
}

.service-center {
  font-size: 16px;
  line-height: 24px;
  letter-spacing: -0.8px;
  color: #151515;
}
.service-number {
  font-family: Roboto;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  color: #151515;
}
.operating-hours {
  font-size: 13px;
  line-height: 20px;
  letter-spacing: -0.65px;
  color: #767676;
}

.popup-content {
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;

  .close-button {
    font-weight: 500;
    font-size: 14px;
    line-height: 50px;
    text-align: right;
    letter-spacing: -0.7px;
    cursor: pointer;
  }
  .popup-body {
    height: 185px;
    .header {
      font-weight: 500;
      font-size: 22px;
      line-height: 36px;
      text-align: center;
      letter-spacing: -1.1px;
      color: #151515;
    }
    .sub-header {
      width: 224px;
      font-size: 16px;
      line-height: 24px;
      text-align: center;
      letter-spacing: -0.8px;
      color: #5a5a5a;
      padding: 8px 0px 20px;
    }
    button {
      width: 280px;
      font-weight: 500;
      font-size: 15px;
      line-height: 50px;
      text-align: center;
      letter-spacing: -0.8px;
      color: #ffffff;
      background: #2cb3ff;
      cursor: pointer;
      border-radius: 4px;
      border: none;
    }
  }
}
</style>
