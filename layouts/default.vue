<template>
  <v-app id="inspire">
    <div v-if="$auth.loggedIn">
      <v-navigation-drawer v-model="drawer" app>
        <!--      -->
        <v-list>
          <!--   Home  Start-->
          <v-list-item
            v-for="(item, i) in homes"
            :key="i"
            :to="item.to"
            router
            exact
          >
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title v-text="item.title" />
            </v-list-item-content>
          </v-list-item>
          <v-divider
            class=""
            horizontal
          ></v-divider>
          <!-- Home  End -->
           <!--   Layouts part     -->
          <v-list>
            <v-list-item
              v-for="(item, i) in layouts"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-action>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title v-text="item.title" />
              </v-list-item-content>
            </v-list-item>
          </v-list>
          <!--   Layouts End     -->
          <!--   Widge Start     -->
          <v-list>
            <v-list-item
              v-for="(item, i) in widgets"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-action>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title v-text="item.title" />
              </v-list-item-content>
            </v-list-item>
          </v-list>
          <!--   Widge End     -->
          <!--        Post Start -->
          <v-list-group no-action sub-group>
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon>mdi-post</v-icon> Post
                </v-list-item-title>
              </v-list-item-content>
            </template>

            <v-list-item
              v-for="(item, i) in posts"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-icon>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item>
          </v-list-group>
          <!-- Post Part End -->
          <!-- Category Part -->
          <v-list-group no-action sub-group>
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon>mdi-dialpad</v-icon> Category
                </v-list-item-title>
              </v-list-item-content>
            </template>

            <v-list-item
              v-for="(item, i) in categories"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-icon>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item>
          </v-list-group>
          <!-- Category Part End -->
          <!--        Tag Part -->
          <v-list-group no-action sub-group>
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon>mdi-tag</v-icon> Tag
                </v-list-item-title>
              </v-list-item-content>
            </template>

            <v-list-item
              v-for="(item, i) in tags"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-icon>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item>
          </v-list-group>
          <!--        Tag Part End -->
          <!--        Seo Part -->
          <v-list-group no-action sub-group>
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon>mdi-web</v-icon> SEO
                </v-list-item-title>
              </v-list-item-content>
            </template>

            <v-list-item
              v-for="(item, i) in seos"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-icon>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item>
          </v-list-group>
          <!--        Seo Part End -->
         
          <!--   Social part     -->
          <v-list-group no-action sub-group>
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon>mdi-link</v-icon> Social
                </v-list-item-title>
              </v-list-item-content>
            </template>

            <v-list-item
              v-for="(item, i) in social"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-icon>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item>
          </v-list-group>
          <!--   Social part End     -->
          <!-- Image part start -->
          <v-list>
            <v-list-item
              v-for="(item, i) in items"
              :key="i"
              :to="item.to"
              router
              exact
            >
              <v-list-item-action>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-action>
              <v-list-item-content>
                <v-list-item-title v-text="item.title" />
              </v-list-item-content>
            </v-list-item>
          </v-list>
          <!-- Image part end -->
        </v-list>
        <!--      -->
      </v-navigation-drawer>
    </div>
    <v-app-bar app>
      <div v-if="$auth.loggedIn">
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      </div>
      <v-toolbar-title>Voice TV</v-toolbar-title>
      <v-spacer></v-spacer>
      <!--      image log-->
      <v-menu bottom min-width="200px" rounded offset-y v-if="$auth.loggedIn">
        <template v-slot:activator="{ on }">
          <v-btn icon x-large v-on="on" class="mr-2">
            <v-avatar color="brown" size="48">
              <v-img
                lazy-src="https://picsum.photos/id/11/10/6"
                max-height="150"
                max-width="250"
                src="https://cdn.vuetifyjs.com/images/cards/girl.jpg"
              ></v-img>
            </v-avatar>
          </v-btn>
        </template>
        <v-card>
          <v-list-item-content class="justify-center">
            <div class="mx-auto text-center">
              <h3>{{ $auth.user.name }}</h3>
              <v-img
                lazy-src="https://picsum.photos/id/11/10/6"
                max-height="150"
                max-width="250"
                src="https://cdn.vuetifyjs.com/images/cards/girl.jpg"
              ></v-img>
              <br />
              <h3>{{ $auth.user.name }}</h3>
              <p class="text-caption mt-1">
                {{ $auth.user.email }}
              </p>
              <v-divider class="my-3"></v-divider>
              <v-btn depressed rounded text> Edit Account </v-btn>
              <v-divider class="my-3"></v-divider>
              <v-btn depressed rounded text @click="$auth.logout()">
                Logout
              </v-btn>
            </div>
          </v-list-item-content>
        </v-card>
      </v-menu>
      <!--      image log end-->
    </v-app-bar>

    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import VuetifyLogo from "../components/VuetifyLogo.vue";
export default {
  components: {
    VuetifyLogo,
  },
  data: () => ({
    
    drawer: null,
    homes: [
      {
        icon: "mdi-apps",
        title: "Dashboard",
        to: "",
      },
    ],
    posts: [
      {
        icon: "mdi-note",
        title: "Add Post",
        to: "/post/addpost",
      },
      {
        icon: "mdi-note-check",
        title: "Post List",
        to: "/post/post",
      },
    ],
    categories: [
      {
        icon: "mdi-menu",
        title: "Add Category",
        to: "/category/addcategory",
      },
      {
        icon: "mdi-menu-open",
        title: "Category List",
        to: "/category/category",
      },
    ],
    tags: [
      {
        icon: "mdi-tag-plus",
        title: "Add Tag",
        to: "/tag/addtag",
      },
      {
        icon: "mdi-tag",
        title: "Tag List",
        to: "/tag/tag",
      },
    ],
    seos: [
      {
        icon: "mdi-web-plus",
        title: "Add Seo",
        to: "/seo/addseo",
      },
      {
        icon: "mdi-web-check",
        title: "Seo List",
        to: "/seo/seo",
      },
    ],
    layouts: [
      {
        icon: "mdi-layers",
        title: "Layouts",
        to: "/layout/list",
      },
      // {
      //   icon: 'mdi-layers-edit',
      //   title: 'Customize Layout',
      //   to: '/layout/customize'
      // },
    ],
    widgets: [
      {
        icon: "mdi-widgets",
        title: "Widgets",
        to: "/widget/list",
      },
      // {
      //   icon: 'mdi-layers-edit',
      //   title: 'Widgets Layout',
      //   to: '/widget/update'
      // },
    ],
    items: [
      // {
      //   icon: "mdi-image",
      //   title: "Image",
      //   to: "/image/image",
      // },

      // {
      //   icon: 'mdi-page-layout-body',
      //   title: 'Widgets',
      //   to: '/layout/widgets'
      // },

      // {
      //   icon: 'mdi-login',
      //   title: 'Register',
      //   to: '/register'
      // },
    ],
    social: [
      {
        icon: "mdi-link-variant-plus",
        title: "Add Social",
        to: "/social/addSocial",
      },
      {
        icon: "mdi-link-variant",
        title: "Social List",
        to: "/social/social",
      },
    ],
  }),
};
</script>

<style>
.v-list-group__header {
  position: relative;
}

.v-list-group__header__prepend-icon {
  position: absolute;
  right: 20px;
}

.v-application--is-ltr
  .v-list-group--no-action.v-list-group--sub-group
  > .v-list-group__items
  > .v-list-item {
  padding-left: 45px;
}

.v-navigation-drawer .v-list-item__title .v-icon {
  margin-right: 28px;
}

.v-application--is-ltr .v-list-group--sub-group .v-list-group__header {
  padding-left: 16px;
}
</style>
