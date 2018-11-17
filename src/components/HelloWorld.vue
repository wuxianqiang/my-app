<template>
  <div>
    <base-table :titleList="titleList" :dataList="dataList" class="table">
      <!-- <template slot-scope="slotProps">
        <span v-if="slotProps.title.key==='name'">
          <el-button>默认按钮</el-button>
        </span>
        <span v-else>{{slotProps.value[slotProps.title.key]}}</span>
      </template> -->
    </base-table>
  </div>
</template>

<script>
import BaseTable from './BaseTable'

export default {
  components: {
    BaseTable
  },
  data () {
    return {
      titleList: [
        {
          key: 'name',
          text: '姓名',
          align: 'left'
        },
        {
          key: 'age',
          text: '年龄',
          width: '50px'
        },
        {
          key: 'sex',
          text: '性别',
          filter: (item) => {
            return item.sex ? '男' : '女'
          }
        },
        {
          key: 'html',
          text: '操作',
          htmlArray: [
            {
              htmlString: '<a href="javascript:;">删除</a>',
              clickEvent: (item) => {
                console.log(item)
              }
            }
          ]
        }
      ],
      dataList: [
        {
          name: '张三',
          age: 18,
          sex: 0
        },
        {
          name: '李四',
          age: 18,
          sex: 1
        }
      ]
    }
  }
}
</script>

<style lang="less" scoped>
.table {
  width: 500px;
}
</style>
