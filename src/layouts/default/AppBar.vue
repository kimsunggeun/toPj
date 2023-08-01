
<template>
  <v-app-bar flat>
    <v-row align="center" justify="center">
      <v-col cols="10">
        <v-row align="center">
          <v-col cols="2">
            <v-app-bar-title>
              <v-icon icon="mdi-circle-slice-6" />
              Essentials Preset
            </v-app-bar-title>
          </v-col>
          <v-col cols="3">
            <v-text-field
              density="compact"
              variant="solo"
              label="Search templates"
              append-inner-icon="mdi-magnify"
              single-line
              hide-details
            ></v-text-field>
          </v-col>
          <v-col cols="1" style="overflow: hidden">
            <div ref="topDiv">
              <p>{{ sliceArr.rank }} {{ sliceArr.country }}</p>
            </div>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-app-bar>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    // const hotListEvent = () => {
    //   console.log(
    //     topDiv.value.childElementCount,
    //     "topDiv.value.childElementCount"
    //   );

    //   UpText.value.transform = "translateY(-50%)";
    // };

    const margin = ref(0);

    const topDiv = ref(null);

    const UpText = ref({
      color: "",
      transition: "all 2s",
      transform: "",
    });

    const hotList = ref([
      {
        rank: "1",
        country: "제주도",
      },
      {
        rank: "2",
        country: "xxx",
      },
      {
        rank: "3",
        country: "ddd",
      },
      {
        rank: "4",
        country: "xzvc",
      },
    ]);

    let cnt = -1;
    let sliceArr = ref([
      {
        rank: "",
        country: "",
      },
    ]);

    let rankRolling = () => {
      cnt += 1;
      sliceArr.value = hotList.value[cnt];
      if (cnt >= hotList.value.length) {
        if (sliceArr.value == undefined) {
          sliceArr.value = {
            rank: "",
            country: "순위 확인용",
          };
        }
        cnt = -1;
      }
    };

    return {
      hotList,
      sliceArr,
      UpText,
      rankRolling,
      topDiv,
      margin,
    };
  },

  mounted() {
    this.rankRolling();
    setInterval(() => {
      this.rankRolling();
    }, 3000);
  },
};
</script>
