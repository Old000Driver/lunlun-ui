<template>
  <div class="layout">
    <Topnav :toggle-menu-button-visible="true" class="nav"/>
    <div class="content">
      <transition name="fade" mode="out-in">
        <aside v-if="menuVisible">
          <h2>文档</h2>
          <ol>
            <li >
              <router-link to="/doc/Intro">介绍
              </router-link>
            </li>
            <li >
              <router-link to="/doc/install">安装
              </router-link>
            </li>
            <li >
              <router-link to="/doc/get-started">开始使用
              </router-link>
            </li>
            <li >
              <router-link to="/doc/switch">Switch 组件
              </router-link>
            </li>
            <li >
              <router-link to="/doc/button">Button 组件
              </router-link>
            </li>
            <li >
              <router-link to="/doc/dialog">Dialog 组件
              </router-link>
            </li>
            <li>
              <router-link to="/doc/tabs">Tabs 组件
              </router-link>
            </li>
          </ol>
        </aside>
      </transition>
      <main>
        <router-view></router-view>
      </main>
    </div>
  </div>
</template>
<script lang="ts">
import Topnav from '../components/Topnav.vue';

import {inject, Ref} from 'vue';

export default {
  components: {Topnav},
  setup() {
    const menuVisible = inject<Ref<boolean>>('menuVisible');
    return {menuVisible};
  }
};
</script>

<style lang="scss">
$asideIndex: 10;


.layout {
  display: flex;
  flex-direction: column;
  height: 100vh;

  > .nav {
    flex-shrink: 0;
  }

  > .content {
    flex-grow: 1;
    padding-top: 60px;
    padding-left: 156px;
    @media (max-width: 500px) {
      padding-left: 0;
    }
  }
}

.content {
  display: flex;

  > aside {
    flex-shrink: 0;
  }

  > main {
    flex-grow: 1;
    padding: 16px;
    background: white;
  }
}


aside {
  box-shadow: 0 10px 10px #bfbfbf;
  z-index: $asideIndex;
  background: #f5f5f5;
  width: 150px;
  padding: 16px 0;
  position: fixed;
  top: 3.2rem;
  left: 0;
  height: 100%;
  bottom: 0;

  > h2 {
    margin-bottom: 4px;
    padding: 4px 16px;
  }

  > ol {
    > li {
      > a {
        display: block;
        padding: 4px 16px;
        text-decoration: none;
      }

      .router-link-active {
        background: white;
      }
    }
  }
}

.fade-enter-from{
  transform: translateX(-150px);
}

.fade-enter-active, {
  transition:ease-in-out 0.25s;

}

.fade-enter-to {
  transform: translateX(0);
}
.fade-leave-active {
  transition: ease-in-out 0.25s;
}

.fade-leave-to {
  transform: translateX(-150px);
}


main {
  overflow: auto;
}
</style>
