<template>
  <div class="easy-table">
    <div class="easy-table_thead" ref="box">
      <table class="easy-table__box">
        <colgroup>
          <col
            v-for="(item, index) in titleList"
            :key="index"
            :width="item.width?item.width:''"
          />
        </colgroup>
        <thead>
          <tr>
            <th
              ref="th"
              v-for="(item, index) in titleList"
              :key="index"
              class="easy-table__th"
              :align="item.align?item.align:'center'"
            >
              <span>{{item.text}}</span>
            </th>
          </tr>
        </thead>
      </table>
    </div>

    <div class="easy-table_tbody">
      <table class="easy-table__box">
        <colgroup>
          <col
            v-for="(item, index) in titleList"
            :key="index"
            :width="thWidth[index]"
          />
        </colgroup>
        <thead>
          <tr
            class="easy-table__tr"
            v-for="(value, index) in dataList"
            :key="index"
            :class="{'easy-table__dark': (index+1)%2===0}"
          >
            <td
              v-for="(title, index) in titleList"
              :key="index"
              class="easy-table__td"
              :align="title.align?title.align:'center'"
            >
              <template>
                <!-- 通过函数处理值 -->
                <span v-if="title.filter">
                  {{title.filter(value)}}
                </span>
                <!-- 默认显示列表值 -->
                <span v-else>
                  <slot :value="value" :title="title">
                    {{value[title.key]}}
                  </slot>
                </span>
              </template>
              <template v-if="title.key==='html'">
                <!-- 可以绑定HTML格式 -->
                <span
                  v-for="(item, index) in title.htmlArray"
                  :key="index"
                  v-html="item.htmlString"
                  @click="()=>item.clickEvent(value)"
                >
                </span>
              </template>
            </td>
          </tr>
        </thead>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    titleList: {
      type: Array,
      default () {
        return {
          text: '姓名',
          key: name
        }
      }
    },
    dataList: {
      type: Array,
      default () {
        return {
          name: '张三'
        }
      }
    }
  },
  data () {
    return {
      thWidth: []
    }
  },
  methods: {
    _formatWidth () {
      let thWidth = []
      let el = this.$refs.th
      for (const th of el) {
        thWidth.push(th.offsetWidth)
      }
      this.thWidth = thWidth
    }
  },
  mounted () {
    this._formatWidth()
  }
}
</script>

<style lang="less" scoped>
.easy-table {
  font-size: 14px;
  color: #606266;
  word-break: break-all;

  &__td {
    padding: 12px;
    border-right: 1px solid #E7E7E7;
    border-bottom: 1px solid #E7E7E7;

  }

  &__th {
    padding: 12px;
    border-right: 1px solid #E7E7E7;
    background: rgba(233, 233, 233, 0.6);
  }

  &__dark {
    background: #fafafa;
  }

  &__tr {
    transition: all 0.3s;
    &:hover {
      background: rgba(233, 233, 233, 0.6);
    }
  }

  &__box {
    table-layout: fixed;
    border-collapse: collapse;
    border-spacing: 0;
    border-spacing: 0;
    width: 100%;
    border-left: 1px solid #E7E7E7;
    border-top: 1px solid #E7E7E7;
  }
}
</style>
