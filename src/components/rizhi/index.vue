<template>
  <el-table :data="tableData" style="width: 100%" :span-method="arraySpanMethod">
    <el-table-column label="值班日志" align='center'>
      <el-table-column label="岗位 \ 班次" align='center' prop='label'></el-table-column>
      <el-table-column label="白班" align='center'>
        <el-table-column label="值班长" align='center'>
          <template slot-scope="scope">
            <el-select v-if='scope.row.type===1' v-model="white.duty.one.name" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
            <el-time-picker v-if='scope.row.type===2' value-format='HH:mm:ss' v-model="white.duty.one.time" placeholder="时间" style="width:100%">
            </el-time-picker>
            <template v-if='scope.row.type===3'>
              <el-radio v-model="white.isOk" label="0">正常</el-radio>
              <el-radio v-model="white.isOk" label="1">异常</el-radio>
            </template>
            <el-input v-if='scope.row.type===4' type="textarea" :rows="4" placeholder="请输入内容" v-model="white.notOkDesc">
            </el-input>
            <el-input v-if='scope.row.type===5' type="textarea" :rows="2" placeholder="请输入内容" v-model="white.remark">
            </el-input>
          </template>
        </el-table-column>
        <el-table-column label="维护岗" align='center'>
          <template slot-scope="scope">
            <el-select v-if='scope.row.type===1' v-model="white.duty.two.name" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
            <el-time-picker v-if='scope.row.type===2' value-format='HH:mm:ss' v-model="white.duty.two.time" placeholder="时间" style="width:100%">
            </el-time-picker>
            <template v-if='scope.row.type===3'>
              <el-radio v-model="black.isOk" label="0">正常</el-radio>
              <el-radio v-model="black.isOk" label="1">异常</el-radio>
            </template>
            <el-input v-if='scope.row.type===4' type="textarea" :rows="4" placeholder="请输入内容" v-model="black.notOkDesc">
            </el-input>
            <el-input v-if='scope.row.type===5' type="textarea" :rows="2" placeholder="请输入内容" v-model="black.remark">
            </el-input>
          </template>
        </el-table-column>
        <el-table-column label="1岗" align='center'>
          <template slot-scope="scope">
            <el-select v-if='scope.row.type===1' v-model="white.duty.p1.name" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
            <el-time-picker v-if='scope.row.type===2' value-format='HH:mm:ss' v-model="white.duty.p1.time" placeholder="时间" style="width:100%">
            </el-time-picker>
          </template>
        </el-table-column>
        <el-table-column label="2岗" align='center'>
          <template slot-scope="scope">
            <el-select v-if='scope.row.type===1' v-model="white.duty.p2.name" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
            <el-time-picker v-if='scope.row.type===2' value-format='HH:mm:ss' v-model="white.duty.p2.time" placeholder="时间" style="width:100%">
            </el-time-picker>
          </template>
        </el-table-column>

      </el-table-column>
      <el-table-column label="夜班" align='center'>
        <el-table-column label="值班长" align='center'>
          <template slot-scope="scope">
            <el-select v-if='scope.row.type===1' v-model="black.duty.one.name" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
            <el-time-picker v-if='scope.row.type===2' value-format='HH:mm:ss' v-model="black.duty.one.time" placeholder="时间" style="width:100%">
            </el-time-picker>
          </template>
        </el-table-column>
        <el-table-column label="维护岗" align='center'>
          <template slot-scope="scope">
            <el-select v-if='scope.row.type===1' v-model="black.duty.two.name" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
            <el-time-picker v-if='scope.row.type===2' value-format='HH:mm:ss' v-model="black.duty.two.time" placeholder="时间" style="width:100%">
            </el-time-picker>
            <template v-if='scope.row.type===3'>
              <el-radio v-model="radio" label="0">正常</el-radio>
              <el-radio v-model="radio" label="1">异常</el-radio>
            </template>
            <el-input v-if='scope.row.type===4' type="textarea" :rows="4" placeholder="请输入内容" v-model="textarea">
            </el-input>
            <el-input v-if='scope.row.type===5' type="textarea" :rows="2" placeholder="请输入内容" v-model="textarea">
            </el-input>
          </template>
        </el-table-column>
        <el-table-column label="1岗" align='center'>
          <template slot-scope="scope">
            <el-select v-if='scope.row.type===1' v-model="black.duty.p1.name" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
            <el-time-picker v-if='scope.row.type===2' value-format='HH:mm:ss' v-model="black.duty.p1.time" placeholder="时间" style="width:100%">
            </el-time-picker>
          </template>
        </el-table-column>
        <el-table-column label="2岗" align='center'>
          <template slot-scope="scope">
            <el-select v-if='scope.row.type===1' v-model="black.duty.p2.name" multiple placeholder="请选择">
              <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
            <el-time-picker v-if='scope.row.type===2' value-format='HH:mm:ss' v-model="black.duty.p2.time" placeholder="时间" style="width:100%">
            </el-time-picker>
          </template>
        </el-table-column>

      </el-table-column>

    </el-table-column>

  </el-table>
</template>

<script>
const initTableData = [
  {
    label: '值班员',
    type: 1
  },
  {
    label: '到岗时间',
    type: 2
  },
  {
    label: '工作情况',
    type: 3
  },
  {
    label: '异常描述',
    type: 4
  },

  {
    label: '备注',
    type: 5
  }
]
export default {
  data() {
    return {
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
      textarea: '',
      value1: '',
      value2: '',
      radio: '1',
      white: {
        duty: {
          one: {
            name: ['张'],
            time: ''
          },
          two: {
            name: ['张'],
            time: ''
          },
          p1: {
            name: ['张'],
            time: ''
          },
          p2: {
            name: ['张'],
            time: ''
          }
        },
        isOk: '0',
        notOkDesc: '',
        remark: ''
      },
      black: {
        duty: {
          one: {
            name: ['张'],
            time: ''
          },
          two: {
            name: ['张'],
            time: ''
          },
          p1: {
            name: ['张'],
            time: ''
          },
          p2: {
            name: ['张'],
            time: ''
          }
        },
        isOk: '0',
        notOkDesc: '',
        remark: ''
      },
      tableData: initTableData
    }
  },
  methods: {
    arraySpanMethod({ row, column, rowIndex, columnIndex }) {
      if (rowIndex >= 2) {
        if (columnIndex >= 1) {
          return [1, 4]
        }
      }
    }
  }
}
</script>