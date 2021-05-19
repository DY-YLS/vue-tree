<style lang="scss" scoped>
.main {
  display: flex;
  height: 100%;

  .tree-menu {
    height: 100%;
    width: 180px;
    margin-right: 5px;
  }

  .right-content {
    // 随便设置一个比较小的宽度，防止表格自动横向增长
    width: 140px;
    height: inherit;
    flex: 1;

    .query-area {
    }

    .table-area {

    }
  }
}
</style>
<template>
  <div class="main">
    <div class="tree-menu">
      <TreeFolderList :data="treeList"
                      :selected="selected"
                      nodeName="menuName" @switchClick="switchClick"
                      @clickTitle="clickTitle"
                      @dbClickTitle="dbClickTitle"
      ></TreeFolderList>
    </div>
  </div>
</template>

<script>
import TreeFolderList from "../components/TreeFolderList";

export default {
  name: "DataSourceViewsTree",
  components: {TreeFolderList},
  data() {
    return {
      selected: {},
      treeList: [
            {
              "id": 51,
              "menuCode": "priority",
              "menuName": "优先级",
              "description": "",
              "sort": 1,
              "parentCode": "",
              "children": [
                {
                  "id": 52,
                  "menuCode": "1",
                  "menuName": "低",
                  "description": "",
                  "sort": 1,
                  "parentCode": "priority",
                  "children": []
                },
                {
                  "id": 53,
                  "menuCode": "2",
                  "menuName": "中低",
                  "description": "",
                  "sort": 2,
                  "parentCode": "priority",
                  "children": []
                },
                {
                  "id": 54,
                  "menuCode": "3",
                  "menuName": "中",
                  "description": "",
                  "sort": 3,
                  "parentCode": "priority",
                  "children": []
                },
                {
                  "id": 55,
                  "menuCode": "4",
                  "menuName": "中高",
                  "description": "",
                  "sort": 4,
                  "parentCode": "priority",
                  "children": []
                },
                {
                  "id": 56,
                  "menuCode": "5",
                  "menuName": "高",
                  "description": "",
                  "sort": 5,
                  "parentCode": "priority",
                  "children": []
                }
              ]
            },
            {
              "id": 57,
              "menuCode": "目录1",
              "menuName": "目录1",
              "description": "",
              "sort": 2,
              "parentCode": "",
              "children": [
                {
                  "id": 58,
                  "menuCode": "目录2",
                  "menuName": "目录2",
                  "description": "",
                  "sort": 2,
                  "parentCode": "目录1",
                  "children": []
                }
              ]
            }
      ],
    }
  },
}
</script>


