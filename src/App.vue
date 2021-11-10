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
                  :titleProp="title"
                  :authorProp="author"
                  :descriptionProp="description"
                  @updateTitle="updateTitle"
                  @updateAuthor="updateAuthor"
                  @updateDescription="updateDescription"
              />
              <v-col class="d-flex mx-0 px-0" cols="12" sm="6">
                <v-select
                    v-model="trealetType"
                    :items="trealetTypes"
                    item-text="type"
                    item-value="index"
                    label="Trealet type"
                    outlined
                ></v-select>
              </v-col>

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
    title: "Chủ đề của Trealet",
    author: "Tác giả",
    description: "Nội dung miêu tả",
    trealetType: 2,
    itemList: [
      {
        number: 1,
        item: "12345",
      },
      {
        number: 2,
        item: "56789",
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

    getUsableItemList() {
      if (this.trealetType == 1) {
        // Grid trealet has an item list of array of objects
        return this.itemList.map((obj) => ({
          item: +obj.item,
          trealet: obj.trealet,
        }));
      } else if (this.trealetType == 2) {
        // Slide trealet has an item list of array of numbers
        return this.itemList.map((obj) => +obj.item);
      }
    },

    exportList() {
      const exportObj = {
        trealet: {
          exec: "streamline",
          title: this.title,
          author: this.author,
          desc: this.description,
          items: this.getUsableItemList(),
        },
      };

      // TO DO:
      // EXPORT FILE HERE
      const data = JSON.stringify(exportObj, null, 2);
      let FileSaver = require('file-saver');
      let blob = new Blob([data], {type: "text/plain;charset=utf-8"});
      FileSaver.saveAs(blob, "test.trealet");
      console.log(data);
    },
  },
};
</script>
