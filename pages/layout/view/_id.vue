<template>
  <v-container>
    <v-sheet v-if="tree!==null">
      <!-- {{ widget_setting }} -->
      <v-sheet v-if="tree.nodes">
        <Tree  :nodes="tree.nodes" :depth="0" :tag="tree.tag" :class="tree.class" :id="tree.section_id" :layout_id="this.$route.params.id" :widget_setting="widget_setting"></Tree>
      </v-sheet>
    </v-sheet>
    <v-sheet v-else>
      Layout not Found
    </v-sheet>
  </v-container>
</template>

<script>
  //import layout from 'assets/layout.json'
  export default {
    name: "test",
    tree: '',
    widget_setting: '',
    data() {
      return {
        //layout: layout,
        tree: {},
      }
    },

    async asyncData(context) {
      const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
      const tree = await context.$axios
        .get('/layouts/' + context.params.id + '/edit', { headers: { Authorization: AuthStr } });
       const widget_setting = await context.$axios
        .get('/layout-widgets/' + context.params.id, { headers: { Authorization: AuthStr } });
      // console.log('Tree: ', tree.data.data['structure']);
      // console.log('Widget Setting: ', widget_setting.data.data);
      return { tree: tree.data.data['structure'], widget_setting: widget_setting.data.data};
    },
  }
</script>