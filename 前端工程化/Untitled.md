table组件

```vue
<!--
 * @Description:
 * @Version: 2.0
 * @Autor: zhang-jinghui
 * @Date: 2021-05-21 16:14:07
 * @LastEditors: zhang-jinghui
 * @LastEditTime: 2021-05-21 17:21:13
-->
<template>
 <el-table
      :data="tableData"
      :span-method="objectSpanMethod"
      border
      style="width: 100%; margin-top: 20px">
      <el-table-column
        v-for="(item, index) in columnConfig"
        :key="index"
        :prop="item.prop"
        :label="item.label">
        <template slot-scope="scope">
          <!-- 读 -->
          <template v-if="canEdit">
            {{ scope.row[item.prop] }}
          </template>
          <!-- 写 -->
          <template v-else>
            <el-input @change="getNewData" size="small" v-model="scope.row[item.prop]" placeholder="请输入内容"></el-input>
          </template>
        </template>
      </el-table-column>
    </el-table>
</template>

<script>
export default {
    name: 'TabYearTarget',
    data () {
        return {
        }
    },
    props: {
        // 能否编辑
        canEdit: {
            type: Boolean,
            default: false
        },
        // 是否能合并单元格
        canSpan: {
            type: Boolean,
            default: false
        },
        // 第一列要合并的垂直方向的单元格的数量
        columnOneRowSpan: {
            type: Number,
            default: 8
        },
        // 第一列要合并的垂直方向的单元格的数量
        columnTwoRowSpan: {
            type: Number,
            default: 2
        },
        // 行配置
        columnConfig: {
            type: Array,
            default: () => [
                { label: 'ID', prop: 'id' },
                { label: '姓名', prop: 'name' },
                { label: '数字1', prop: 'amount1' },
                { label: '数字2', prop: 'amount2' },
                { label: '数字3', prop: 'amount3' }
            ]
        },
        // 表格数据
        tableData: {
            type: Array,
            default: () => [{
                id: '12987122',
                name: '王小虎',
                amount1: '234',
                amount2: '3.2',
                amount3: 10
            }, {
                id: '12987123',
                name: '王小虎',
                amount1: '165',
                amount2: '4.43',
                amount3: 12
            }, {
                id: '12987123',
                name: '王小虎',
                amount1: '165',
                amount2: '4.43',
                amount3: 12
            }, {
                id: '12987123',
                name: '王小虎',
                amount1: '165',
                amount2: '4.43',
                amount3: 12
            }, {
                id: '12987123',
                name: '王小虎',
                amount1: '165',
                amount2: '4.43',
                amount3: 12
            }, {
                id: '12987123',
                name: '王小虎',
                amount1: '165',
                amount2: '4.43',
                amount3: 12
            }, {
                id: '12987124',
                name: '王小虎',
                amount1: '324',
                amount2: '1.9',
                amount3: 9
            }, {
                id: '12987125',
                name: '王小虎',
                amount1: '621',
                amount2: '2.2',
                amount3: 17
            }]
        }
    },
    methods: {
        objectSpanMethod ({ row, column, rowIndex, columnIndex }) {
            if (!this.canSpan) {
                return {
                    rowspan: 1,
                    colspan: 1
                }
            }
            if (columnIndex === 0) {
                // 只有第一列进行单元格合并
                if (rowIndex % this.columnOneRowSpan === 0) {
                    return {
                        rowspan: this.columnOneRowSpan,
                        colspan: 1
                    }
                } else {
                    return {
                        rowspan: 0,
                        colspan: 0
                    }
                }
            }
            if (columnIndex === 1) {
                // 只有第二列进行单元格合并
                if (rowIndex % this.columnTwoRowSpan === 0) {
                    return {
                        rowspan: this.columnTwoRowSpan,
                        colspan: 1
                    }
                } else {
                    return {
                        rowspan: 0,
                        colspan: 0
                    }
                }
            }
        },
        getNewData (nv) {
            this.$emit('getTableNewData', this.tableData)
        }
    }
}
</script>

<style>

</style>

```

导航组件

```vue
<!--
 * @Description:
 * @Version: 2.0
 * @Autor: zhang-jinghui
 * @Date: 2021-05-21 17:30:21
 * @LastEditors: zhang-jinghui
 * @LastEditTime: 2021-05-21 17:57:54
-->
<template>
<div>
  <div class="tab-contain">
    <ul class="tabs">
      <li class="tab-item"><span class="tab-item-label">日报名称</span></li>
      <li class="tab-item"><span class="tab-item-label">日报名称</span></li>
      <li class="tab-item"><span class="tab-item-label">日报名称</span></li>
    </ul>
  </div>
  <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="用户管理" name="first"></el-tab-pane>
      <el-tab-pane label="配置管理" name="second"></el-tab-pane>
      <el-tab-pane label="角色管理" name="third"></el-tab-pane>
      <el-tab-pane label="定时任务补偿" name="fourth"></el-tab-pane>
    </el-tabs>
    </div>
</template>

<script>
export default {
    name: 'TabNavigation',
    data () {
        return {
            activeName: 'first'
        }
    },
    methods: {
        handleClick (nv) {
            console.log(nv)
        }
    }
}
</script>

<style scoped lang='scss'>
.tab-contain {
  width: 100%;
  border-bottom: 2px solid #E0E3EA;
  .tabs {
    display: inline-block;
      // margin: 4px 20px;
      // border-bottom: 1px solid black;
      .tab-item {
        float: left;
        padding: 0 20px;
        &:first-child {
          padding: 0;
        }
        // 控制文案
        .tab-item-label {
          font-size: 14px;
          font-weight: 600;
        }
      }
  }
}
</style>

```





