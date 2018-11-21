<template>
  <div>
    <el-table row-key="date" ref="table" border :data="tableData" style="width: 100%" id='table'>
      <el-table-column label="值班时间" align='center'>
        <el-table-column label='日期 \ 岗位' align='center' width="140">
          <template slot-scope="scope">
            <span>{{ scope.row.day }}</span>
            <span> （{{ scope.row.week }}）</span>
          </template>
        </el-table-column>
      </el-table-column>
      <el-table-column label="0:00-8:30" align='center'>
        <el-table-column label='带班' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.one1 | optionsSelect}}</span>
          </template>
        </el-table-column>
        <el-table-column label='维护' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.one2 | optionsSelect}}</span>
          </template>
        </el-table-column>
        <el-table-column label='值班' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.one3 | optionsSelect}}</span>
          </template>
        </el-table-column>
      </el-table-column>
      <el-table-column label='8:30-18:00' align='center'>
        <el-table-column label='带班' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.two1 | optionsSelect}}</span>
          </template>
        </el-table-column>
        <el-table-column label='维护' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.two2 | optionsSelect}}</span>
          </template>
        </el-table-column>
        <el-table-column label='值班' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.two3 | optionsSelect}}</span>
          </template>
        </el-table-column>
      </el-table-column>
      <el-table-column label='18:00-0:00' align='center'>
        <el-table-column label='带班' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.three1 | optionsSelect}}</span>
          </template>
        </el-table-column>
        <el-table-column label='维护' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.three2 | optionsSelect}}</span>
          </template>
        </el-table-column>
        <el-table-column label='值班' align='center'>
          <template slot-scope="scope">
            <span>{{ scope.row.three3 | optionsSelect}}</span>
          </template>
        </el-table-column>
      </el-table-column>
      <el-table-column label='休息' align='center'>
        <template slot-scope="scope">
          <span>{{ scope.row.rest | optionsSelect}}</span>
        </template>
      </el-table-column>

    </el-table>
    <el-row style="margin-top:30px" type="flex" justify="end">
      <el-button type="primary" @click="exportExcel">导出Excel</el-button>
    </el-row>
  </div>
</template>

<script>
import Sortable from 'sortablejs'
import FileSaver from 'file-saver'
import XLSX from 'xlsx'

import DATALIST from './tableList.js'
const originOptions = [
  {
    value: '01',
    label: '朱'
  },
  {
    value: '02',
    label: '争'
  },
  {
    value: '03',
    label: '杉'
  },
  {
    value: '04',
    label: '伟'
  },
  {
    value: '05',
    label: '培'
  },
  {
    value: '06',
    label: '谢'
  },
  {
    value: '07',
    label: '路'
  },
  {
    value: '08',
    label: '峰'
  },
  {
    value: '09',
    label: '雷'
  },
  {
    value: '10',
    label: '涛'
  }
]
export default {
  data() {
    return {
      tableData: DATALIST
    }
  },
  filters: {
    optionsSelect: function(arr) {
      let newArr = originOptions.filter(item => {
        return arr.includes(item.value)
      })
      let selectedArr = newArr.map(item => item.label)
      return selectedArr.join('\\')
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
  },
  methods: {
    exportExcel() {
      /* generate workbook object from table */
      let wb = XLSX.utils.table_to_book(document.querySelector('#table'))
      /* get binary string as output */
      let wbout = XLSX.write(wb, {
        bookType: 'xlsx',
        bookSST: true,
        type: 'array'
      })
      try {
        FileSaver.saveAs(
          new Blob([wbout], { type: 'application/octet-stream' }),
          '播出科值班表.xlsx'
        )
      } catch (e) {
        if (typeof console !== 'undefined') console.log(e, wbout)
      }
      return wbout
    }
  }
}
</script>