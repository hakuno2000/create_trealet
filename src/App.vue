<template>
  <v-app>
    <v-app-bar app color="white">
      <div class="d-flex align-center">
        <v-img
            alt="Trealet Logo"
            class="shrink mr-2"
            contain
            src="@/assets/logo.png"
            transition="scale-transition"
            width="150"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
          href="https://hcloud.trealet.com/apps_dev/btl/nhom03/Streamline/?trealet=/albums/Nhom03/app/hoihoaphuchung.trealet"
          target="_blank"
          text
      >
        <span class="mr-2">View Trealet</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <div style="display: flex; justify-content: center">
        <div style="width: 80%">
          <v-form>
            <v-container>
              <Info
                  :filenameProp="filename"
                  :titleProp="title"
                  :authorProp="author"
                  :descriptionProp="description"
                  :quizProp="quiz"
                  @updateFilename="updateFilename"
                  @updateTitle="updateTitle"
                  @updateAuthor="updateAuthor"
                  @updateDescription="updateDescription"
                  @updateQuiz="updateQuiz"
              />
<!--              <v-col class="d-flex mx-0 px-0" cols="12" sm="6">-->
<!--                <v-select-->
<!--                    v-model="trealetType"-->
<!--                    :items="trealetTypes"-->
<!--                    item-text="type"-->
<!--                    item-value="index"-->
<!--                    label="Trealet type"-->
<!--                    outlined-->
<!--                ></v-select>-->
<!--              </v-col>-->

              <GridItemList
                  v-if="trealetType == 1"
                  :itemListProp="itemList"
                  @updateList="updateList"
              />
              <SlideItemList
                  v-if="trealetType == 2"
                  :itemListProp="itemList"
                  @updateList="updateList"
              />

              <v-divider class="my-12"></v-divider>

              <v-btn
                  class="ml-auto mb-3 d-block"
                  color="primary"
                  dark
                  large
                  @click="exportList"
              >
                Export
              </v-btn>
            </v-container>
          </v-form>
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import Info from "@/components/Info";
import SlideItemList from "@/components/SlideItemList";
import GridItemList from "@/components/GridItemList";

export default {
  name: "App",

  components: {
    Info,
    SlideItemList,
    GridItemList,
  },

  data: () => ({
    filename: "hoihoaphuchung",
    title: "Hội hoạ Phục Hưng",
    author: "Nhóm 03",
    description: "Thời kì Phục Hưng thường được người ta miêu tả ở khoảng thế kỉ thứ 16 nhưng ngay từ thế kỉ thứ 14, những mầm mống đầu tiên của phong trào này đã bắt đầu nhem nhóm từ Ý(Quatrocento – 1400). Trong thời kì này, sự trỗi dậy của tầng lớp giàu có – tiền thân của giai cấp tư sản sau này đã tạo ra một làn sóng xây dựng một nền văn hóa mới để chống lại giai cấp phong kiến lạc hậu. Phục Hưng có gốc từ tiếng Pháp (Renaissance – nghĩa là sự tái sinh), điều này ám chỉ tinh thần của nó là thời kỳ làm sống lại những tinh hoa văn hóa của Hy Lạp và La Mã cổ.",
    trealetType: 2,
    quiz: "quiz.trealet",
    itemList: [
      {
        item: "21322",
        detail: {
          exec: "streamline",
          title: "Leonardo da Vinci",
          desc: "Leonardo da Vinci (1452-1519) là một họa sĩ, nhà điêu khắc, kiến trúc sư, nhạc sĩ, bác sĩ, kỹ sư, nhà giải phẫu, nhà sáng tạo và triết học tự nhiên. Với tài năng trời phú, ông được mọi người ví như một thiên tài toàn năng người Ý với danh hiệu Leonardo da Vinci tác phẩm nghệ thuật.",
          items: [11274, 11242, 16194, 16202, 16210, 16218, 16226, 16234, 16258, 16274, 16282, 16290, 16298],
        },
      },
      {
        item: "21354",
        detail: {
          exec: "streamline",
          title: "Masaccio",
          desc: "Masaccio (1401-1428), tên khai sinh Tommaso di Ser Giovanni di Simone,  là họa sĩ Ý vĩ đại đầu tiên của giai đoạn thế kỷ thứ 15 của thời kỳ Phục hưng Ý. Theo Vasari, Masaccio là họa sĩ xuất sắc nhất trong thế hệ của ông vì kỹ năng tái tạo hình khối sống động như thật và các phong trào cũng như ý nghĩa thuyết phục của tạo hình ba chiều.",
          items: [16434, 16418, 16426],
        },
      },
    ],
    trealetTypes: [
      {
        index: 1,
        type: "Grid",
      },
      {
        index: 2,
        type: "Slide",
      },
    ],
  }),

  watch: {
    trealetType(val) {
      if (val == 1) {
        this.itemList = [
          {
            number: 1,
            item: "12345",
            trealet: "example1.trealet",
          },
          {
            number: 2,
            item: "56789",
            trealet: "example2.trealet",
          },
        ];
      } else if (val == 2) {
        this.itemList = [
          {
            number: 1,
            item: "12345",
          },
          {
            number: 2,
            item: "56789",
          },
        ];
      }
    },
  },

  methods: {
    updateFilename(value) {
      this.filename = value;
    },

    updateTitle(value) {
      this.title = value;
    },

    updateAuthor(value) {
      this.author = value;
    },

    updateDescription(value) {
      this.description = value;
    },

    updateList(value) {
      this.itemList = value;
    },

    updateQuiz(value) {
      this.quiz = value
    },

    getUsableItemList() {
      if (this.trealetType == 1) {
        // Grid trealet has an item list of array of objects
        return this.itemList.map((obj) => ({
          item: +obj.item,
          trealet: obj.trealet,
        }));
      } else if (this.trealetType == 2) {
        // Slide trealet has an item list of array of numbers
        return this.itemList.map((obj) => ({
          item: +obj.item,
          detail: obj.detail,
        }));
      }
    },

    exportList() {
      const exportObj = {
        trealet: {
          exec: "streamline",
          title: this.title,
          author: this.author,
          desc: this.description,
          quiz: this.quiz,
          items: this.getUsableItemList(),
        },
      };

      // TO DO:
      // EXPORT FILE HERE
      const data = JSON.stringify(exportObj, null, 2);
      let FileSaver = require('file-saver');
      let blob = new Blob([data], {type: "text/plain;charset=utf-8"});
      FileSaver.saveAs(blob, this.filename+".trealet");
      console.log(data);
    },
  },
};
</script>
