<template>
  <v-select v-bind:items="ui_widgets" label="UI Widget" item-value="text" v-model="selectedWidget" @input="$emit('widgetSelected', selectedWidget)" single-line>
    <!-- Add icon in the selection -->
    <template slot="item" slot-scope="data">
      <v-list-tile-avatar>
        <v-icon>{{data.item.icon}}</v-icon>
      </v-list-tile-avatar>
      <v-list-tile-content>
        <v-list-tile-title v-html="data.item.text"></v-list-tile-title>
      </v-list-tile-content>
    </template>
  </v-select>
</template>

<script>
export default {
  data() {
    return {
      ui_widgets: [
        {
          text: 'Text field',
          icon: 'text_fields',
        },
        {
          text: 'Checkboxes',
          icon: 'check_box',
        },
        {
          text: 'Drop-down',
          icon: 'arrow_drop_down_circle',
        },
        {
          text: 'Multiple choice',
          icon: 'radio_button_checked',
        },
      ],
      selectedWidget: '',
    };
  },
};
</script>
