<template>
  <v-app>
    <v-app-bar
        app
        color="white"
    >
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
          <Info/>
          <ItemList/>
        </div>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import Info from "@/components/Info";
import ItemList from "@/components/ItemList";

export default {
  name: 'App',

  components: {
    Info,
    ItemList,
  },

  data: () => ({
  }),
};
</script>
