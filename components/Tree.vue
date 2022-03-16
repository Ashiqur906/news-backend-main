<template>
  <component :is="tag" :class="classes">
    <v-card v-if="label" color="grey lighten-4" flat min-height="200px" tile>
      <v-toolbar dense>
        <v-toolbar-title>{{ label }}</v-toolbar-title>

        <v-spacer></v-spacer>
        <!-- {{ section_id }} -->
        <v-btn
          v-if="widget_setting.map(function(e) { return e.widget_space_id; }).indexOf(section_id) < 0"
          icon
          :to="{ name: 'layout-update-layout_id-widget_space_id-id', params: { layout_id: layout_id, widget_space_id: section_id },}"
        >
          <v-icon>mdi-plus</v-icon>
        </v-btn>
      </v-toolbar>

      <v-card-text class="tree-text">
        <v-row v-for="(data, index) in widget_setting" :key="index">
          <v-card-text v-if="section_id === data.widget_space_id">
            <v-row>
              <!-- <v-spacer></v-spacer> -->
              <v-btn
              icon
              :to="{ name: 'layout-update-layout_id-widget_space_id-id', params: { layout_id: layout_id, widget_space_id: section_id, id: data.id },}"
            >
              <v-icon small class="tree-text">mdi-pencil</v-icon>
            </v-btn></v-row>
            <br>
            <v-row>
              <v-col class="text-left">
                <div class="m-1" v-if="data.widget_settings.widget_type !== null"><v-chip color="green">Widget Type :</v-chip> {{ data.widget_name }} </div>
                <!-- <div v-if="data.widget_settings.taxonomy !== null"><v-chip>Taxonomy : </v-chip>{{ data.widget_settings.taxonomy }} </div> -->
                <!-- <div v-if="data.widget_settings.data_limit !== null"><v-chip color="green">Data Limit :</v-chip> {{ data.widget_settings.data_limit }} </div> -->
                <div v-if="data.widget_settings.data !== null"><v-chip>Data :</v-chip> {{ data.widget_settings.data }}</div>
              </v-col>
            </v-row>

            
          </v-card-text>
        </v-row>
      </v-card-text>
    </v-card>
    <tree
      v-for="(node, index) in nodes"
      :key="index"
      :layout_id="layout_id"
      :nodes="node.nodes"
      :label="node.label"
      :tag="node.tag"
      :class="node.class"
      :depth="depth + 1"
      :section_id="node.section_id"
      :id="node.section_id"
      :widget_setting="widget_setting"
    >
    </tree>
  </component>
</template>

<script>
export default {
  
  props: [
    "label",
    "nodes",
    "depth",
    "tag",
    "classes",
    "section_id",
    "layout_id",
    "widget_setting",
  ],
  name: "Tree",
};
</script>

<style scoped>
.tree-text {
  color: black !important;
}
</style>