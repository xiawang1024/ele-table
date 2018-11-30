<template>
  <div>
    <el-table
      :data="tableData"
      style="width: 100%"
      :span-method="arraySpanMethod"
    >
      <el-table-column
        label="值班日志"
        align='center'
      >
        <el-table-column
          label="岗位 \ 班次"
          align='center'
          prop='label'
        ></el-table-column>
        <el-table-column
          :label="dutyTitle"
          align='center'
        >
          <el-table-column
            label="值班长"
            align='center'
          >
            <template slot-scope="scope">
              <el-select
                v-if='scope.row.type===1'
                v-model="dutyData.duty.one.name"
                multiple
                placeholder="请选择"
                style="width:100%"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
              <el-time-picker
                v-if='scope.row.type===2'
                value-format='HH:mm:ss'
                v-model="dutyData.duty.one.time"
                placeholder="时间"
                style="width:100%"
              >
              </el-time-picker>
              <template v-if='scope.row.type===3'>
                <el-radio
                  v-model="dutyData.isOk"
                  label="0"
                >正常</el-radio>
                <el-radio
                  v-model="dutyData.isOk"
                  label="1"
                >异常</el-radio>
              </template>
              <el-input
                v-if='scope.row.type===4'
                type="textarea"
                :rows="4"
                placeholder="请输入内容"
                v-model="dutyData.notOkDesc"
              >
              </el-input>
              <el-input
                v-if='scope.row.type===5'
                type="textarea"
                :rows="2"
                placeholder="请输入内容"
                v-model="dutyData.remark"
              >
              </el-input>
            </template>
          </el-table-column>
          <el-table-column
            label="维护岗"
            align='center'
          >
            <template slot-scope="scope">
              <el-select
                v-if='scope.row.type===1'
                v-model="dutyData.duty.two.name"
                multiple
                placeholder="请选择"
                style="width:100%"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
              <el-time-picker
                v-if='scope.row.type===2'
                value-format='HH:mm:ss'
                v-model="dutyData.duty.two.time"
                placeholder="时间"
                style="width:100%"
              >
              </el-time-picker>

            </template>
          </el-table-column>
          <el-table-column
            label="1岗"
            align='center'
          >
            <template slot-scope="scope">
              <el-select
                v-if='scope.row.type===1'
                v-model="dutyData.duty.p1.name"
                multiple
                placeholder="请选择"
                style="width:100%"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
              <el-time-picker
                v-if='scope.row.type===2'
                value-format='HH:mm:ss'
                v-model="dutyData.duty.p1.time"
                placeholder="时间"
                style="width:100%"
              >
              </el-time-picker>
            </template>
          </el-table-column>
          <el-table-column
            label="2岗"
            align='center'
          >
            <template
              slot-scope="scope"
              style="width:100%"
            >
              <el-select
                v-if='scope.row.type===1'
                v-model="dutyData.duty.p2.name"
                multiple
                placeholder="请选择"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
              <el-time-picker
                v-if='scope.row.type===2'
                value-format='HH:mm:ss'
                v-model="dutyData.duty.p2.time"
                placeholder="时间"
                style="width:100%"
              >
              </el-time-picker>
            </template>
          </el-table-column>

        </el-table-column>

      </el-table-column>

    </el-table>
    <el-row
      style="margin-top:30px"
      type="flex"
      justify="end"
    >
      <el-button
        type="primary"
        @click="submitRizhi"
      >提交</el-button>
    </el-row>
  </div>

</template>

<script>
const initTableData = [
  {
    label: "值班员",
    type: 1
  },
  {
    label: "到岗时间",
    type: 2
  },
  {
    label: "工作情况",
    type: 3
  },
  {
    label: "异常描述",
    type: 4
  },

  {
    label: "备注",
    type: 5
  }
];
export default {
  data() {
    return {
      dutyTitle: "白班/夜班",
      options: [
        {
          value: "选项1",
          label: "黄金糕"
        },
        {
          value: "选项2",
          label: "双皮奶"
        },
        {
          value: "选项3",
          label: "蚵仔煎"
        },
        {
          value: "选项4",
          label: "龙须面"
        },
        {
          value: "选项5",
          label: "北京烤鸭"
        }
      ],

      dutyData: {
        duty: {
          one: {
            name: ["张"],
            time: ""
          },
          two: {
            name: ["张"],
            time: ""
          },
          p1: {
            name: ["张"],
            time: ""
          },
          p2: {
            name: ["张"],
            time: ""
          }
        },
        isOk: "0",
        notOkDesc: "",
        remark: ""
      },

      tableData: initTableData
    };
  },
  methods: {
    arraySpanMethod({ row, column, rowIndex, columnIndex }) {
      if (rowIndex >= 2) {
        if (columnIndex >= 1) {
          return [1, 4];
        }
      }
    },
    submitRizhi() {
      alert("tijiao");
    }
  }
};
</script>