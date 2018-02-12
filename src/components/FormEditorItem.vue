<template>
  <v-card :class="[{border: addBorder}]" @click.native="addBorder = true">
    <v-card-text primary-title>
      <v-container fluid>
        <v-layout row justify-space-between>
          <v-flex xs5>
            <v-text-field label="Field Name" v-model="formItem.FieldName" single-line>
            </v-text-field>
          </v-flex>
          <v-flex xs3>
            <v-select v-bind:items="dataTypes" label="Data Type" v-model="formItem.DataType" single-line>
            </v-select>
          </v-flex>
          <v-flex xs3>
            <select-widget @widgetSelected="formItem.UIWidget = $event"></select-widget>
          </v-flex>
        </v-layout>
        <v-text-field v-if="formItem.UIWidget == 'Text field'" value="Input text" disabled>
        </v-text-field>
        <template v-if="formItem.UIWidget == 'Checkboxes' || formItem.UIWidget == 'Multiple choice'">
          <v-layout row v-for="i in optionCounter">
            <v-flex xs9>
              <v-text-field label="Add Option" single-line :prepend-icon="prependIcon[formItem.UIWidget]"></v-text-field>
            </v-flex>
            <v-spacer></v-spacer>
            <button-with-tooltip @click.native="optionCounter--" icon='close' tooltip='Remove'></button-with-tooltip>
          </v-layout>
          <v-btn flat color="primary" @click.native="optionCounter++">Add Other</v-btn>
        </template>
      </v-container>
    </v-card-text>
    <v-divider></v-divider>
    <v-card-actions class="pt-2 pb-0">
      <v-container>
        <v-layout row>
          <v-spacer></v-spacer>
          <v-flex xs2>
            <v-switch class="input-group--full-width" label="Required" v-model="formItem.IsRequired">
            </v-switch>
          </v-flex>
          <v-flex xs2>
            <v-switch label="Display on Card" v-model="formItem.DisplayOnCard"></v-switch>
          </v-flex>
          <button-with-tooltip icon='delete' tooltip='Delete'></button-with-tooltip>
        </v-layout>
        <v-fab-transition>
          <v-btn color="indigo darken-4" fab dark small absolute bottom right>
            <v-icon>add</v-icon>
          </v-btn>
        </v-fab-transition>
      </v-container>
    </v-card-actions>
  </v-card>
</template>

<script>
import SelectWidget from './FormElements/SelectWidget';
import ButtonWithTooltip from './FormElements/ButtonWithTooltip';

export default {
  props: ['selected'],
  components: {
    SelectWidget,
    ButtonWithTooltip,
  },
  created() {
    console.log(this.selected);
  },
  data() {
    return {
      formItem: {
        FieldName: '',
        UIWidget: '',
        DataType: '',
        IsRequired: false,
        DisplayOnCard: true,
      },
      prependIcon: {
        Checkboxes: 'check_box_outline_blank',
        'Multiple choice': 'radio_button_unchecked',
      },
      dataTypes: ['String', 'Number', 'Decimal', 'Boolean'],
      addBorder: false,
      optionCounter: 1,
    };
  },
  methods: {
    addFormElement(event) {
      this.addBorder = true;
    },
  },
};
</script>

<style scoped>
.border {
  border: 1px solid #eee;
  border-left-width: 5px;
  border-left-color: #428bca;
  transition: box-shadow 0.25s cubic-bezier(0, 0, 0.2, 1);
}
</style>
