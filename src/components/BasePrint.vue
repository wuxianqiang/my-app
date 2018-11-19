<template>
  <div class="base-table">
    <table width="95%" cellpadding="0" cellspacing="0" style="table-layout:fixed;page-break-after:always">
      <thead>
        <tr>
          <th colspan="3" class="base-table__title">成绩单</th>
        </tr>
        <tr>
          <th class="base-table__name">语文</th>
          <th class="base-table__name">数学</th>
          <th class="base-table__name">英语</th>
        </tr>
      </thead>
      <tbody class="base-table__body">
        <tr v-for="(item, index) in 5" :key="index">
          <td class="base-table__name">99</td>
          <td class="base-table__name">88</td>
          <td class="base-table__name">99</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td colspan="3" class="base-table__foot"></td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="less" scoped>
.base-table {
  width: 80mm;
  margin: 0 auto;

  &__foot {
    border-bottom: 1px dashed #666;
  }

  &__title {
    border-bottom: 1px dashed #666;
    vertical-align: top;
    text-align: center;
    line-height: 48px;
  }

  &__name {
    border-collapse: collapse;
    text-align: center;
    word-wrap: break-word;
    word-break: break-all;
    font-size: 8px;
    padding: 10px 5px;
    vertical-align: top;
    text-align: center;
  }
}
</style>
