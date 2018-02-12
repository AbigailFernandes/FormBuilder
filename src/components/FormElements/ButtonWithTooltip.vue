<template>
    <v-tooltip bottom>
        <v-btn icon slot="activator">
            <v-icon>{{icon}}</v-icon>
        </v-btn>
        <span>{{tooltip}}</span>
    </v-tooltip>
</template>

<script>
export default {
  props: ['icon', 'tooltip'],
};
</script>

