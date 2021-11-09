<template>
  <v-form>
    <v-container>
      <v-row>
        <v-toolbar
            flat
        >
          <v-toolbar-title>Trealet Info</v-toolbar-title>
          <v-divider
              class="mx-4"
              inset
              vertical
          ></v-divider>
        </v-toolbar>
      </v-row>
      <v-row>
        <v-col
            cols="12"
            sm="6"
        >
          <v-text-field
              v-model="title"
              label="Title"
              outlined
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col
            cols="12"
            sm="6"
        >
          <v-text-field
              v-model="author"
              label="Author"
              outlined
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-container fluid>
          <v-textarea
              name="input-7-1"
              filled
              label="Description"
              auto-grow
              outlined
              value="Nội dung miêu tả"
          ></v-textarea>
        </v-container>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  data: () => ({
    title: 'Chủ đề của Trealet',
    author: 'Tác giả',
  }),
}
</script>

<style scoped>

</style>