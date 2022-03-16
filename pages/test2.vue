<template>
<v-container>
  <!-- {{ tree2 }} -->
  <v-sheet v-if="tree.nodes">
    <Tree  :nodes="tree.nodes" :depth="0" :tag="tree.tag" :class="tree.class" :id="tree.section_id"></Tree>
  </v-sheet>
  <!-- <v-sheet v-if="tree.nodes">
    <Tree  :nodes="tree.nodes" :depth="0" :tag="tree.tag" :class="tree.class" :id="tree.section_id"></Tree>
  </v-sheet> -->
</v-container>
</template>

<script>
//import layout from 'assets/layout.json'
export default {
  name: "test",
  tree: '',
  data() {
    return {
      //layout: layout,
      tree: {},
      tree2: {
    tag: "div",
    class: "",
    image: "preview.jpg",
    label: "root",
    node: [{
      tag: "header",
      class: "voice-header",
      label: "Header",
      section_id: "voice-header1"
    }, {
      tag: "section",
      class: "container",
      label: "Marquee",
      section_id: "marquee-section"
    }, {
      tag: "section",
      class: "container",
      node: [{
        tag: "div",
        class: "row",
        node: [{
          tag: "div",
          class: "col-3",
          nodes: [{
            tag: "div",
            class: "row",
            nodes: [{
              tag: "div",
              class: "col-12",
              label: "Main Section 1",
              section_id: "asdh234"
            }, {
              tag: "div",
              class: "col-12",
              label: "Main Section 2",
              section_id: "agt32ewd"
            }]
          }]
        }, {
          tag: "div",
          class: "col-5",
          label: "Main Section 3",
          section_id: "398qeowia"
        }, {
          tag: "div",
          class: "col-4",
          nodes: [{
            tag: "div",
            class: "row",
            nodes: [{
              tag: "div",
              class: "col-12",
              label: "Live TV",
              section_id: "hery9as"
            }, {
              tag: "div",
              class: "col-12",
              label: "Main Section 4",
              section_id: "2893uoi"
            }]
          }]
        }]
      }]
    }, {
      tag: "section",
      class: "container",
      nodes: [{
        tag: "div",
        class: "row",
        nodes: [{
          tag: "div",
          class: "col-5",
          label: "Two Column Two Rows News Widget",
          section_id: "28y43equih"
        }, {
          tag: "div",
          class: "col-4",
          label: "সব খবর",
          section_id: "28y3ewui"
        }, {
          tag: "div",
          class: "col-3",
          label: "Advertisement Widget Mujib 100",
          section_id: "e9283uei"
        }]
      }]
    }, {
      tag: "section",
      class: "container",
      nodes: [{
        tag: "div",
        class: "row",
        nodes: [{
          tag: "div",
          class: "col-6",
          label: "বিনোদন",
          section_id: "wr42y98ew"
        }, {
          tag: "div",
          class: "col-3",
          label: "অপরাধ",
          section_id: "w42y8ewuhi"
        }, {
          tag: "div",
          class: "col-3",
          label: "জেলার সংবাদ",
          section_id: "2984ew"
        }]
      }]
    }, {
      tag: "section",
      class: "container",
      nodes: [{
        tag: "div",
        class: "row",
        nodes: [{
          tag: "div",
          class: "col-6",
          label: "রাজনীতি",
          section_id: "43rewrt"
        }, {
          tag: "div",
          class: "col-3",
          label: "সারাদেশ",
          section_id: "3298oisa"
        }, {
          tag: "div",
          class: "col-3",
          label: "Advertisement widget",
          section_id: "y6u56ryt"
        }]
      }]
    }, {
      tag: "section",
      class: "container",
      label: "Advertisement Section",
      section_id: "24983ew"
    }, {
      tag: "section",
      class: "container",
      label: "ভিডিও সংবাদ",
      section_id: "5ersdfa3"
    }, {
      tag: "section",
      class: "container",
      nodes: [{
        tag: "div",
        class: "row",
        nodes: [{
          tag: "div",
          class: "col-3",
          label: "বিশ্ব",
          section_id: "2948ewoids"
        }, {
          tag: "div",
          class: "col-3",
          label: "খেলার খবর",
          section_id: "2938wuoids"
        }, {
          tag: "div",
          class: "col-6",
          label: "ছবি গ্যালারি",
          section_id: "slknjdk2983"
        }]
      }]
    }, {
      tag: "footer",
      class: "container",
      label: "Footer",
      section_id: "Footer-1"
    }],
    section_id: "root",
    layout_name: "Voice TV",
    layout_slug: "voice-tv"
  },
    }
  },
  
  asyncData(context) {
  const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
  return context.$axios
    //.get(context.env.apiRoot + 'post-slug?slug=' + encodeURI(context.params.slug))
    .get('layouts/4', { headers: { Authorization: AuthStr } })
    .then((res) => {
      if (res.data.length === 0 || res.data.error) {
        throw({ statusCode: 404, message: 'Posts not found' })
      }
      console.log(res.data.data['structure']);
      return { tree: res.data.data['structure'] }
    })
    .catch(error => {
      if (error.response) {
        // Request made and server responded
        //this.errorResponse = error.response.data;
        this.errorCode = error.response.status;
      } else if (error.request) {
        // The request was made but no response was received
        //console.log(error.request);
      } else {
        // Something happened in setting up the request that triggered an Error
        return {error: error.message};
        return context.error({ statusCode: 500, message: error.message })
      }
    });
  },
}
</script>
