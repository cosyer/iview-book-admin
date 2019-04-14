<template>
  <div
    class="sidebar-menu-con"
    :class="{'sidebar-menu-sk':state.hideMenuText}"
  >
    <div class="logo-con">
      <img
        src=""
        alt=""
      >
    </div>
    <!-- 展开-->
    <Menu
      @on-open-change="openChange"
      :open-names="openNames"
      :accordion="true"
      v-show="!state.hideMenuText"
      theme="light"
      slot="content"
      class="menu-po"
      @on-select="selectHandler"
      :active-name="currPageName"
    >
      <MenuItem
        :name="m.routerName"
        v-for="(m,index) in activeMenus"
        :key="index"
      >
      <Icon
        class="menu-icon"
        :type="m.icon"
      ></Icon>
      <span class="layout-text">{{m.name}}</span>
      </MenuItem>
    </Menu>
    <!--缩放-->
    <div
      class="font-center"
      v-show="state.hideMenuText"
      v-for="m in state.menus"
      :key="m.path"
    >
      <Button
        @click="changeMenu(m.routerName)"
        class="font-center-btn"
        v-if="!m.hide&&!(m.children&&m.children.length>0)"
        type="text"
      >
        <Icon
          v-if="m.icon"
          class="menu-icon"
          :type="m.icon"
        ></Icon>
      </Button>
      <Dropdown
        v-if="!m.hide&&m.children&&m.children.length>0"
        placement="right-start"
        @on-click="changeMenu"
      >
        <Button
          class="font-center-btn"
          type="text"
        >
          <Icon
            v-if="m.icon"
            class="menu-icon"
            :type="m.icon"
          ></Icon>
        </Button>
        <DropdownMenu
          style="width: 150px;"
          slot="list"
        >
          <template v-for="(child, i) in m.children">
            <DropdownItem
              style="width: 150px;"
              :name="child.routerName"
              :key="i"
            >
              {{child.name}}
            </DropdownItem>
          </template>
        </DropdownMenu>
      </Dropdown>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  name: "sidebar-menu",
  data() {
    return {
      home: "Workbench"
    };
  },
  computed: mapState({
    state: state => state.menu,
    isHome(state) {
      let { userPermission = "" } = state.users;
      return userPermission.indexOf("sys.index") !== -1;
    },
    // 展开的菜单数组
    openNames(state) {
      let { openedArr } = state.menu;
      return openedArr;
    },
    // 选中的父菜单和子菜单 格式 A?B
    currPageName: state => state.menu.currPageName,
    // 有效的菜单(v-if不要和v-for混用,v-for具有比v-if更高的优先级,这意味着v-if将分别重复运行于每个v-for循环中)
    activeMenus: state => {
      return state.menu.menus.filter(item => !item.hide);
    }
  }),
  created() {},
  methods: {
    selectHandler(name) {
      document.body.click();
      this.$router.push({ name });
    },
    changeMenu(name) {
      this.$router.push({ name });
    },
    openChange(openedArr) {
      this.$store.commit("menu/openedArr", openedArr);
    }
  }
};
</script>

<style lang="less">
@import "./sidebarMenu.less";
</style>