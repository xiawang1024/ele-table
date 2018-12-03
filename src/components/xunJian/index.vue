<template>
  <div>
    <el-row
      type="flex"
      justify="end"
      style="margin-bottom:30px;"
    >
      <el-button
        type='primary'
        @click="addIns"
      >
        新增记录
      </el-button>
      <el-button type='primary'>
        提交记录
      </el-button>
    </el-row>
    <el-table
      :data="tableData"
      border
      style="width: 100%"
    >
      <template v-for="column of headData">
        <el-table-column
          :prop="column.prop"
          :label="column.label"
          :key='column.prop'
          align="center"
        >
          <template slot-scope="scope">
            <RenderWx :obj='scope.row[column.prop]'>
            </RenderWx>
          </template>
        </el-table-column>
      </template>
      <el-table-column
        fixed="right"
        label="操作"
        width="100"
        align="center"
      >
        <template slot-scope="scope">
          <el-button
            type="danger"
            size="mini"
            @click="removeIns(scope.$index,scope.row)"
          >删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import RenderWx from "./render.vue";
export default {
  components: {
    RenderWx
  },
  data() {
    return {
      headData: [
        {
          prop: "ins0",
          label: "直播机房"
        },
        {
          prop: "ins1",
          label: "工艺电源"
        },
        {
          prop: "ins2",
          label: "USB电源"
        },
        {
          prop: "ins3",
          label: "调音台"
        },
        {
          prop: "ins4",
          label: "转播预听"
        },
        {
          prop: "ins5",
          label: "信号分配"
        },
        {
          prop: "ins6",
          label: "主控机房"
        },
        {
          prop: "ins7",
          label: "直播机房"
        },
        {
          prop: "ins8",
          label: "四选一切换"
        }
      ],
      tableData: [
        //0：文本  1：选项
        {
          ins0: { type: 0, value: "2301" },
          ins1: { type: 1, value: false },
          ins2: { type: 1, value: false },
          ins3: { type: 1, value: false },
          ins4: { type: 1, value: false },
          ins5: { type: 1, value: false },
          ins6: { type: 0, value: "中波" },
          ins7: { type: 0, value: "交通" },
          ins8: { type: 1, value: false },
          ins9: { type: -1, value: false }
        },
        {
          ins0: { type: 0, value: "2302" },
          ins1: { type: 1, value: false },
          ins2: { type: 1, value: false },
          ins3: { type: 1, value: false },
          ins4: { type: 1, value: false },
          ins5: { type: 1, value: false },
          ins6: { type: 0, value: "中波" },
          ins7: { type: 0, value: "交通" },
          ins8: { type: 1, value: false }
        },
        {
          ins0: { type: 0, value: "2303" },
          ins1: { type: 1, value: false },
          ins2: { type: 1, value: false },
          ins3: { type: 1, value: false },
          ins4: { type: 1, value: false },
          ins5: { type: 1, value: false },
          ins6: { type: 0, value: "中波" },
          ins7: { type: 0, value: "交通" },
          ins8: { type: 1, value: false }
        }
      ],
      ins: {
        ins0: { type: 0, value: "" },
        ins1: { type: 1, value: false },
        ins2: { type: 1, value: false },
        ins3: { type: 1, value: false },
        ins4: { type: 1, value: false },
        ins5: { type: 1, value: false },
        ins6: { type: 0, value: "" },
        ins7: { type: 0, value: "" },
        ins8: { type: 1, value: false }
      }
    };
  },

  mounted() {},
  methods: {
    addIns() {
      // let addIns = Object.assign({}, this.ins);
      let addIns = JSON.parse(JSON.stringify(this.ins));

      let newData = [...this.tableData, addIns];

      this.tableData = newData;
    },
    removeIns(index, row) {
      this.tableData.splice(index, 1);
    }
  }
};
</script>