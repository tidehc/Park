<template>
  <mu-flexbox orient="vertical" align="stretch" class="main-layout">
    <mu-appbar :title="name">
      <mu-icon-button icon="menu" @click="toggle(true)" slot="left"/>
      <mu-icon-button icon="more_vert" slot="right"/>
    </mu-appbar>
    <mu-drawer :open="open" :docked="docked" @close="toggle()">
      <mu-paper class="demo-menu">
        <mu-flexbox justify="center" >
            <mu-avatar :class="'drawer-header'" solt="center" :src="require('./../assets/logo.png')" :size="60"/>
        </mu-flexbox>
        <mu-menu @item-click="toggle()">
          <mu-menu-item title="当前停车" leftIcon="local_parking"/>
          <mu-menu-item title="停车记录" leftIcon="person_add"/>
          <mu-menu-item title="账号信息" leftIcon="link"/>
          <mu-divider/>
          <mu-menu-item title="设置" leftIcon="content_copy"/>
          <mu-menu-item title="关于" leftIcon="file_download"/>
        </mu-menu>
      </mu-paper>
    </mu-drawer>
    <router-view></router-view>
  </mu-flexbox>
</template>

<script>
  export default {
    data() {
      return {
        open: false,
        docked: true,
        name: '停车'
      }
    },
    created:function () {
      this.$router.push('/park')

    },
    methods: {
      toggle(flag) {
        this.open = !this.open
        this.docked = !flag
      }
    }
  }
</script>
<style>
  .drawer-header{
    margin: 10px;
  }
  .main-layout{
    height: 100%;
  }
</style>
