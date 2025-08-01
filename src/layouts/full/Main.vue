<script setup lang="ts">
  import { onMounted, ref, shallowRef, watch } from 'vue';
  import { useDisplay } from 'vuetify';
  import sidebarItems from './vertical-sidebar/sidebarItem';
  import NavGroup from './vertical-sidebar/NavGroup/index.vue';
  import NavItem from './vertical-sidebar/NavItem/index.vue';
  import ExtraBox from './vertical-sidebar/extrabox/ExtraBox.vue';
  import Logo from './logo/Logo.vue';
  // Icon Imports
  import { Menu2Icon } from 'vue-tabler-icons';
  // dropdown imports
  import NotificationDD from './vertical-header/NotificationDD.vue';
  import ProfileDD from './vertical-header/ProfileDD.vue';
  import NavCollapse from './vertical-sidebar/NavCollapse/NavCollapse.vue';
  const sidebarMenu = shallowRef(sidebarItems);

  const { mdAndDown } = useDisplay();
  const sDrawer = ref(true);
  onMounted(() => {
    sDrawer.value = !mdAndDown.value; // hide on mobile, show on desktop
  });
  watch(mdAndDown, val => {
    sDrawer.value = !val;
  });
</script>

<template>
  <!------Sidebar-------->
  <v-navigation-drawer
    v-model="sDrawer"
    app
    class="leftSidebar"
    elevation="0"
    left
    :width="270"
  >
    <!---Logo part -->
    <div class="pa-5">
      <Logo />
    </div>
    <!-- ---------------------------------------------- -->
    <!---Navigation -->
    <!-- ---------------------------------------------- -->
    <div>
      <v-list class="pa-6">
        <!---Menu Loop -->
        <template v-for="(item, i) in sidebarMenu">
          <!---Item Sub Header -->
          <NavGroup v-if="item.header" :key="item.title" :item="item" />

          <NavCollapse v-else-if="item.children" class="leftPadding" :item="item" :level="0" />
          <!---Single Item-->
          <NavItem v-else class="leftPadding" :item="item" />
          <!---End Single Item-->
        </template>
      </v-list>
      <div class="pa-4">
        <ExtraBox />
      </div>
    </div>

  </v-navigation-drawer>
  <!------Header-------->
  <v-app-bar class="top-header" elevation="0" height="70">
    <div class="d-flex align-center justify-space-between w-100">
      <div>
        <v-btn
          class="hidden-lg-and-up ms-md-3 ms-sm-5 ms-3 text-muted"
          icon
          size="small"
          variant="flat"
          @click="sDrawer = !sDrawer"
        >
          <Menu2Icon size="20" stroke-width="1.5" />
        </v-btn>
        <!-- Notification -->
        <NotificationDD />
      </div>
      <div>
        <!-- Upgrade button -->
        <v-btn class="mr-2 bg-primary" href="https://adminmart.com/product/modernize-vuetify-vue-admin-dashboard/?ref=56#product-demo-section" target="_blank">Check Pro Template</v-btn>
        <!-- User Profile -->
        <ProfileDD />
      </div>
    </div>
  </v-app-bar>
</template>
