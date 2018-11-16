<template>
  <div>
    <el-table row-key="order" ref="table" border :data="tableData" style="width: 100%">
      <el-table-column label="值班时间" width="150" align='center'>
        <el-table-column prop='order' label='组 \ 岗位' align='center'></el-table-column>
      </el-table-column>
      <!-- <el-table-column label="0:00-8:30" align='center'>
        <el-table-column label='带班' align='center'>
          <template slot-scope="scope">
            <el-select v-model="scope.row.one1" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
          </template>
        </el-table-column>
        <el-table-column label='维护' align='center'>
          <template slot-scope="scope">
            <el-select v-model="scope.row.one2" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
          </template>
        </el-table-column>
        <el-table-column label='值班' align='center'>
          <template slot-scope="scope">
            <el-select v-model="scope.row.one3" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
          </template>
        </el-table-column>
      </el-table-column> -->
      <!-- <el-table-column label='8:30-18:00' align='center'>
        <el-table-column label='带班' align='center'></el-table-column>
        <el-table-column label='维护' align='center'></el-table-column>
        <el-table-column label='值班' align='center'></el-table-column>
      </el-table-column>
      <el-table-column label='18:00-0:00' align='center'>
        <el-table-column label='带班' align='center'></el-table-column>
        <el-table-column label='维护' align='center'></el-table-column>
        <el-table-column label='值班' align='center'></el-table-column>
      </el-table-column> -->
      <TableColumn v-for='timeItem in timeLimitList' :key="timeItem.timer" :tiemTypeOrder='timeItem.timer' :options='options' timeLimit='0:00-8:30'></TableColumn>

      <el-table-column label='休息' align='center'>
        <template slot-scope="scope">
          <el-select v-model="scope.row.rest" multiple placeholder="请选择">
            <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
            </el-option>
          </el-select>
        </template>
      </el-table-column>
      <el-table-column label='操作' align='center'>
        <template slot-scope="scope" v-if='tableLen-1 === scope.$index'>
          <el-button size="mini" @click="handlerAdd(scope.$index, scope.row)">增加</el-button>
        </template>
      </el-table-column>
    </el-table>
    <pre>{{tableData}}</pre>

  </div>
</template>

<script>
import Sortable from 'sortablejs'

import TableColumn from './tableColumn'
export default {
  components: {
    TableColumn
  },
  data() {
    return {
      timeLimitList: [
        //三个时间阶段
        {
          timer: 1,
          value: '0:00-8:30'
        },
        {
          timer: 2,
          value: '8:30-18:00'
        },
        {
          timer: 3,
          value: '18:00-0:00'
        }
      ],
      options: [
        {
          value: '选项1',
          label: '黄金糕'
        },
        {
          value: '选项2',
          label: '双皮奶'
        },
        {
          value: '选项3',
          label: '蚵仔煎'
        },
        {
          value: '选项4',
          label: '龙须面'
        },
        {
          value: '选项5',
          label: '北京烤鸭'
        }
      ],
      tableData: [
        {
          order: '1',
          one1: [],
          one2: [],
          one3: [],
          two1: [],
          two2: [],
          two3: [],
          three1: [],
          three2: [],
          three3: [],
          rest: [],
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          order: '2',
          one1: [],
          one2: [],
          one3: [],
          two1: [],
          two2: [],
          two3: [],
          three1: [],
          three2: [],
          three3: [],
          rest: [],
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          order: '3',
          one1: [],
          one2: [],
          one3: [],
          two1: [],
          two2: [],
          two3: [],
          three1: [],
          three2: [],
          three3: [],
          rest: [],
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        }
      ]
    }
  },
  computed: {
    tableLen: function() {
      return this.tableData.length
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
    isCanAdd(data) {
      let {
        one1,
        one2,
        one3,
        two1,
        two2,
        two3,
        three1,
        three2,
        three3,
        rest
      } = data
      if (
        one1.length == 0 ||
        one2.length == 0 ||
        one3.length == 0 ||
        two1.length == 0 ||
        two2.length == 0 ||
        two3.length == 0 ||
        three1.length == 0 ||
        three2.length == 0 ||
        three3.length == 0 ||
        rest.length == 0
      ) {
        return false
      } else {
        return true
      }
    },
    handlerAdd(index, row) {
      console.log(index, row)
      let isAdd = this.isCanAdd(row)
      if (!isAdd) {
        this.$message.error('错了哦，这是一条错误消息')
        return
      }
      let newRow = {
        order: this.tableLen + 1,
        one1: [],
        one2: [],
        one3: [],
        two1: [],
        two2: [],
        two3: [],
        three1: [],
        three2: [],
        three3: [],
        rest: [],
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }
      this.tableData = [...this.tableData, newRow]
    }
  }
}
</script>