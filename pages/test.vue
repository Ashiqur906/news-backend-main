<template>
    <v-sheet>
      <Tree  :nodes="tree.nodes" :depth="0" :tag="tree.tag" :class="tree.class" :id="tree.section_id"></Tree>
    </v-sheet>
</template>

<script>
  //import layout from 'assets/layout.json'
  let tree = {
    label: 'root',
    tag: 'div',
    class: '',
    section_id: 'root',
    nodes: [
      {
        tag: 'header',
        class: 'voice-header',
        section_id: 'voice-header1',
        label: 'Header',
      },
      {
        tag: 'section',
        class: 'container',
        section_id: 'marquee-section',
        label: 'Marquee',
      },
      {
        tag: 'section',
        class: 'container',
        nodes: [
          {
            tag: 'div',
            class: 'row',
            nodes: [
              {
                tag: 'div',
                class: 'col-3',
                nodes: [
                  {
                    tag: 'div',
                    class: 'row',
                    nodes: [
                      {
                        tag: 'div',
                        class: 'col-12',
                        label: 'Main Section 1',
                        section_id: 'asdh234'
                      },
                      {
                        tag: 'div',
                        class: 'col-12',
                        label: 'Main Section 2',
                        section_id: 'agt32ewd'
                      },
                    ]
                  },
                ]
              },
              {
                tag: 'div',
                class: 'col-5',
                label: 'Main Section 3'
              },
              {
                tag: 'div',
                class: 'col-4',
                nodes: [
                  {
                    tag: 'div',
                    class: 'row',
                    nodes: [
                      {
                        tag: 'div',
                        class: 'col-12',
                        label: 'Live TV',
                        section_id: 'hery9as'
                      },
                      {
                        tag: 'div',
                        class: 'col-12',
                        label: 'Main Section 4',
                        section_id: '2893uoi'
                      },
                    ]
                  },
                ]
              },
            ]
          },
        ]
      },
      {
        tag: 'section',
        class: 'container',
        nodes: [
          {
            tag: 'div',
            class: 'row',
            nodes: [
              {
                tag: 'div',
                class: 'col-5',
                label: 'Two Column Two Rows News Widget',
                section_id: '28y43equih'
              },
              {
                tag: 'div',
                class: 'col-4',
                label: 'সব খবর',
                section_id: '28y3ewui'
              },
              {
                tag: 'div',
                class: 'col-3',
                label: 'Advertisement Widget Mujib 100',
                section_id: 'e9283uei'
              },
            ]
          },
        ]
      },
      {
        tag: 'section',
        class: 'container',
        nodes: [
          {
            tag: 'div',
            class: 'row',
            nodes: [
              {
                tag: 'div',
                class: 'col-6',
                label: 'বিনোদন',
                section_id: 'wr42y98ew'
              },
              {
                tag: 'div',
                class: 'col-3',
                label: 'অপরাধ',
                section_id: 'w42y8ewuhi'
              },
              {
                tag: 'div',
                class: 'col-3',
                label: 'জেলার সংবাদ',
                section_id: '2984ew'
              },
            ]
          },
        ]
      },
      {
        tag: 'section',
        class: 'container',
        nodes: [
          {
            tag: 'div',
            class: 'row',
            nodes: [
              {
                tag: 'div',
                class: 'col-6',
                label: 'রাজনীতি',
                section_id: '43rewrt'
              },
              {
                tag: 'div',
                class: 'col-3',
                label: 'সারাদেশ'
              },
              {
                tag: 'div',
                class: 'col-3',
                label: 'Advertisement widget',
                section_id: 'y6u56ryt'
              },
            ]
          },
        ]
      },
      {
        tag: 'section',
        class: 'container',
        label: 'Advertisement Section',
        section_id: '24983ew'
      },
      {
        tag: 'section',
        class: 'container',
        label: 'ভিডিও সংবাদ',
        section_id: '5ersdfa3'
      },
      {
        tag: 'section',
        class: 'container',
        nodes: [
          {
            tag: 'div',
            class: 'row',
            nodes: [
              {
                tag: 'div',
                class: 'col-3',
                label: 'বিশ্ব'
              },
              {
                tag: 'div',
                class: 'col-3',
                label: 'খেলার খবর'
              },
              {
                tag: 'div',
                class: 'col-6',
                label: 'ছবি গ্যালারি'
              },
            ]
          },
        ]
      },
      {
        tag: 'footer',
        class: 'container',
        label: 'Footer',
        section_id: 'Footer-1'
      },
    ]
  }
    export default {
        name: "test",
        data() {
          return {
            //layout: layout,
            tree: tree,
          }
        },
    }
</script>

<style >
  #root  * {
    border: 1px solid white;
    min-height: 100px;
  }
</style>
