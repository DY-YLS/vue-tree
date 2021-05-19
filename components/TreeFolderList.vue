<style lang="scss" scoped>
.root-list {
  overflow: auto;
  height: 100%;
  width: 100%;
  background-color: white;

  &::-webkit-scrollbar {
    width: 12px;
    height: 12px;

  }

  &::-webkit-scrollbar-thumb {
    border-radius: 0px;
  }
}

li {
  cursor: pointer;
}

.switch {
  display: inline-block;
  width: 18px;
  height: 18px;
  background-image: url("../assets/images/zTreeStandard.png");
  background-repeat: no-repeat;
  user-select: none;
}

.switch-open {
  background-position: -24px -71px;
}

.switch-close {
  background-position: 2px -71px;
}

.folder {
  display: inline-block;
  width: 16px;
  height: 16px;
  background-image: url("../assets/images/zTreeStandard.png");
  background-repeat: no-repeat;
}

.folder-open {
  background-position: -110px -16px;
}

.folder-close {
  background-position: -110px 0;
}

.title {
  display: inline-block;
  padding: 4px 3px 8px 0;
  font-size: 14px;

  .text {
    &:hover {
      text-decoration: underline;
    }

  }
}

.not-last-item {
  background: url("../assets/images/line_conn.gif") 0 0 repeat-y;
}
</style>
<template>

  <ul class="root-list" v-show="isChildrenGreaterZero()  && switchOpen">
    <template v-for="(item,index) in data">
      <TreeFolder v-bind="$attrs" v-on="$listeners" :data="item" :last-item="index==data.length-1"
                  :key="index"></TreeFolder>
    </template>

  </ul>
</template>

<script>
export default {
  name: "TreeFolderList",
  components: {TreeFolder: () => import('./TreeFolder.vue')},
  props: {
    data: {
      type: Array,
    },

  },
  data() {
    return {
      switchOpen: true
    }
  },
  methods: {
    isChildrenGreaterZero() {
      return this.data.length > 0
    },
    switchClick() {
      this.switchOpen = !this.switchOpen
    }
  },
  computed: {
    switchClass() {
      return {
        "switch-open": this.switchOpen,
        "switch-close": !this.switchOpen
      }
    },
    folderClass() {
      return {
        "folder-open": this.switchOpen,
        "folder-close": !this.switchOpen
      }
    },
    notLastItem() {
      return {
        "not-last-item": !this.lastItem
      }
    }
  }
}
</script>

