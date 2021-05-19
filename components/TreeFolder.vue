<style lang="scss" scoped>
.list {
  padding-left: 21px;
  transition: all 1s ease 0s;
}


.not-last-item {
  background: url("../assets/images/line_conn.gif") 0 0 repeat-y;
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

.switch-hidden {
  visibility: hidden;
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

.file {
  background-position: -110px -32px;
}

.title {
  display: inline-block;
  padding: 0px 3px 2px 0;
  font-size: 14px;

  .text {
    &:hover {
      text-decoration: underline;
    }

  }
}

.title-selected {
  background-color: rgba(0, 140, 140, 0.3);
}

.row {
  display: inline-block;
  white-space: nowrap;
}
</style>
<template>
  <li>
    <span class="row">
      <span class="switch" :class="switchClass" @click="switchClick"></span>
      <!-- todo 多组件选中后颜色的选择
      1.用vuex保存
      2.用v-bind="$attrs"层层传递一个保存选中元素的变量
      -->
      <span class="title" :class="titleClass" @click="clickTitle">
          <span class="folder" :class="folderClass"></span>
          <span class="text">{{ data[nodeName] }}</span>
        </span>
    </span>


    <ul class="list" :class="ulClass" v-if="isChildrenGreaterZero() && switchOpen">
      <template v-for="(item,index) in data.children">
        <TreeFolder :nodeName="nodeName"
                    :uniqueName="uniqueName"
                    :selected="selected"
                    v-bind="$attrs" v-on="$listeners"
                    :data="item"
                    :last-item="index==data.children.length-1" :key="index"></TreeFolder>

      </template>
    </ul>

  </li>
</template>

<script>
// 解决单击和双击的冲突
let timer;
let clickCount = 0
export default {
  name: "TreeFolder",
  components: {TreeFolderList: () => import('./TreeFolderList.vue')},
  props: {
    data: {
      type: Object,
    },
    selected: {
      type: Object
    },
    nodeName: {
      type: String,
      default: 'title'
    },
    uniqueName: {
      type: String,
      default: 'id'
    },
    lastItem: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      switchOpen: false
    }
  },
  methods: {
    clickTitle() {
      clearTimeout(timer)
      clickCount++
      timer = setTimeout(() => {

        if (clickCount == 1) {
          this.singleClick()
        } else if (clickCount == 2) {
          this.dbClick()
        }
        clickCount = 0
      }, 300)

    },
    singleClick() {
      this.$emit('clickTitle', this.data)
    },
    dbClick() {
      this.switchOpen = !this.switchOpen
      this.$emit('dbClickTitle', this.data)
    },

    isChildrenGreaterZero() {

      return this.data.children && this.data.children.length > 0
    },
    switchClick() {
      this.switchOpen = !this.switchOpen
      this.$emit('switchClick', this.data, this.switchOpen)
    }
  },

  computed: {
    ulClass() {
      return {
        "not-last-item": !this.lastItem
      }

    },
    switchClass() {
      return {
        "switch-open": this.switchOpen,
        "switch-close": !this.switchOpen,
        "switch-hidden": !this.isChildrenGreaterZero()
      }
    },
    titleClass() {
      return {
        'title-selected': this.selected[this.uniqueName] == this.data[this.uniqueName]
      }
    },
    folderClass() {
      return {
        "folder-open": this.switchOpen,
        "folder-close": !this.switchOpen,
      }
    },
  }
}
</script>

