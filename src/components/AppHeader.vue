<template>
  <div class="hello">
    <v-app id="inspire">
      <v-card color="grey lighten-4" flat>
        <v-toolbar dark color="indigo darken-4" prominent flat extended>
          <v-toolbar-side-icon></v-toolbar-side-icon>
        </v-toolbar>
        <v-layout row>
          <v-flex xs8 offset-xs2>
            <v-card class="card--flex-toolbar">
              <v-toolbar card color="white" prominent>
                <v-toolbar-title class="body-2 grey--text">{{ adapterName }}</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-btn icon>
                  <v-icon>apps</v-icon>
                </v-btn>
                <v-btn icon>
                  <v-icon>more_vert</v-icon>
                </v-btn>
              </v-toolbar>
              <v-divider></v-divider>
              <v-card-title primary-title>
                <v-text-field label="Adapter Name" v-model="adapterName" single-line></v-text-field>
              </v-card-title>
            </v-card>
          </v-flex>
        </v-layout>
        <v-layout v-for="i in formElementsCounter" row @click="selectFormEditorItem(i)">
          <v-flex xs8 offset-xs2>
            <form-editor-item :selected="selectedFormEditorItem[i - 1]"></form-editor-item>
          </v-flex>
        </v-layout>
      </v-card>
    </v-app>
  </div>
</template>

<script>
import FormEditorItem from './FormEditorItem';

export default {
  name: 'AppHeader',
  components: {
    FormEditorItem,
  },
  data() {
    return {
      adapterName: 'Untitled Adapter',
      addBorder: false,
      formElementsCounter: 1,
      selectedFormEditorItem: [false, false],
    };
  },
  methods: {
    selectFormEditorItem(index) {
      // this.selectedFormEditorItem.fill(false);
      this.selectedFormEditorItem[index - 1] = true;
      console.log(this.selectedFormEditorItem);
    },
  },
};
</script>

<style scoped>
.card--flex-toolbar {
  margin-top: -64px;
}
</style>
