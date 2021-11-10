<template>
  <v-data-table
    :headers="headers"
    :items="itemList"
    sort-by="number"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>List of Items</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>
        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="white"
              class="mb-2"
              v-bind="attrs"
              v-on="on"
              style="margin: 5px"
            >
              Add Item
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editedItem.item"
                      label="Id of item"
                      :rules="numberOnly()"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                :disabled="isNotNumber(editedItem.item)"
                @click="save"
              >
                Save
              </v-btn>
              <v-btn color="blue darken-1" text @click="close"> Cancel </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title
              class="text-h5"
              style="display: flex; justify-content: center"
              >Do you want to remove this item?
            </v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm"
                >Confirm</v-btn
              >
              <v-btn color="blue darken-1" text @click="closeDelete"
                >Cancel</v-btn
              >
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon small class="mr-2" @click="editItem(item)"> mdi-pencil </v-icon>
      <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize"> Reset </v-btn>
    </template>
  </v-data-table>
</template>

<script>
export default {
  props: {
    itemListProp: {
      type: Array,
      default: () => [],
    },
  },

  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "No.",
        align: "start",
        sortable: false,
        value: "number",
      },
      { text: "Item Id", value: "item" },
      { text: "Actions", value: "actions", sortable: false },
    ],
    itemList: [],
    editedIndex: -1,
    editedItem: {
      number: 0,
      item: 0,
    },
    defaultItem: {
      number: 0,
      item: 0,
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
    itemList: {
      handler(val) {
        this.$emit("updateList", val);
      },
      deep: true,
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.itemList = this.itemListProp;
    },

    editItem(item) {
      this.editedIndex = this.itemList.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.itemList.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.itemList.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.isNotNumber(this.editedItem.item)) return;

      if (this.editedIndex > -1) {
        Object.assign(this.itemList[this.editedIndex], this.editedItem);
      } else {
        this.itemList.push(this.editedItem);
      }
      this.close();
    },

    isNotNumber(val) {
      return isNaN(val);
    },

    numberOnly() {
      return [(val) => /^[0-9]*$/.test(val) || "Invalid"];
    },
  },
};
</script>

<style scoped>
</style>