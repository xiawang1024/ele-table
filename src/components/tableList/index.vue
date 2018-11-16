<template>
  <div>
    <el-table row-key="date" ref="table" border :data="tableData" style="width: 100%">
      <el-table-column label="值班时间" width="150" align='center'>
        <el-table-column prop='date' label='日期 \ 岗位' align='center'></el-table-column>
      </el-table-column>
      <el-table-column label="0:00-8:30" align='center'>
        <el-table-column label='带班' align='center'></el-table-column>
        <el-table-column label='维护' align='center'></el-table-column>
        <el-table-column label='值班' align='center'></el-table-column>
      </el-table-column>
      <el-table-column label='8:30-18:00' align='center'>
        <el-table-column label='带班' align='center'></el-table-column>
        <el-table-column label='维护' align='center'></el-table-column>
        <el-table-column label='值班' align='center'></el-table-column>
      </el-table-column>
      <el-table-column label='18:00-0:00' align='center'>
        <el-table-column label='带班' align='center'></el-table-column>
        <el-table-column label='维护' align='center'></el-table-column>
        <el-table-column label='值班' align='center'></el-table-column>
      </el-table-column>
      <el-table-column label='休息' align='center'></el-table-column>
      <el-table-column label='备注' align='center'></el-table-column>
    </el-table>

  </div>
</template>

<script>
import Sortable from 'sortablejs'
export default {
  data() {
    return {
      tableData: [
        {
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          date: '2016-05-02',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          date: '2016-05-08',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          date: '2016-05-06',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          date: '2016-05-07',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        }
      ]
    }
  },
  mounted() {
    const table = document.querySelector('.el-table__body-wrapper tbody')
    const self = this
    Sortable.create(table, {
      onEnd({ newIndex, oldIndex }) {
        const targetRow = self.tableData.splice(oldIndex, 1)[0]
        self.tableData.splice(newIndex, 0, targetRow)
      }
    })
  }
}
</script>