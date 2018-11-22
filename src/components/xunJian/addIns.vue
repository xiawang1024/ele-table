<template>
  <div>
    <el-row type="flex" justify="end" style="margin-bottom:30px;">
      <el-button type="primary" @click="addType">新增选项</el-button>
    </el-row>
    <el-table :data="typeList" style="width: 100%" border>
      <el-table-column type="index" width="60" align="center"></el-table-column>
      <el-table-column prop="label" label="巡检选项" width="150">
      </el-table-column>
      <el-table-column label="选项类型">
        <template slot-scope="scope">
          <el-radio v-model="scope.row.type" label="0" border size="medium" :disabled="scope.row.type!=0">文本</el-radio>
          <el-radio v-model="scope.row.type" label="1" border size="medium" :disabled="scope.row.type!=1">选框</el-radio>
        </template>
      </el-table-column>
      <el-table-column label='操作' width="180">
        <template slot-scope="scope">
          <el-button type="primary" size="mini" @click="openEditDialog(scope.$index,scope.row)">编辑</el-button>
          <el-button type="danger" size="mini" @click="openRemoveDialog(scope.$index,scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog title="提示" :visible.sync="removeDialog" width="30%">
      <span>确定删除 "{{dialogText}}" 选项</span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="removeDialog = false">取 消</el-button>
        <el-button type="primary" @click="removeType">确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog title="编辑选项" :visible.sync="editDialog" width="350px">
      <el-form label-position="right" label-width="80px" :model="editTypeData">
        <el-form-item label="巡检选项">
          <el-input v-model="editTypeData.label" clearable></el-input>
        </el-form-item>
        <el-form-item label="选项类型">
          <el-radio-group v-model="editTypeData.type">
            <el-radio label="0" border>文本</el-radio>
            <el-radio label="1" border>选框</el-radio>
          </el-radio-group>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="editDialog = false">取 消</el-button>
        <el-button type="primary" @click="editType">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'addIns',
  data() {
    return {
      dialogIndex: 0,
      dialogText: '',
      editTypeData: {},
      editDialog: false,
      removeDialog: false,
      editDialogType: 0, //0:新增，1：编辑
      typeList: [
        {
          prop: 'ins0',
          label: '直播机房',
          type: '0'
        },
        {
          prop: 'ins1',
          label: '工艺电源',
          type: '1'
        },
        {
          prop: 'ins2',
          label: 'USB电源',
          type: '1'
        },
        {
          prop: 'ins3',
          label: '调音台',
          type: '1'
        },
        {
          prop: 'ins4',
          label: '转播预听',
          type: '1'
        },
        {
          prop: 'ins5',
          label: '信号分配',
          type: '1'
        },
        {
          prop: 'ins6',
          label: '主控机房',
          type: '0'
        },
        {
          prop: 'ins7',
          label: '直播机房',
          type: '0'
        },
        {
          prop: 'ins8',
          label: '四选一切换',
          type: '1'
        }
      ]
    }
  },
  created() {},
  mounted() {},
  methods: {
    addType() {
      this.editDialogType = 0
      this.editTypeData = {
        label: '',
        type: '0'
      }
      this.editDialog = true
    },
    editType() {
      if (this.editDialogType == 1) {
        setTimeout(() => {
          this.editDialog = false
          this.$message({
            message: '恭喜你，修改成功',
            type: 'success'
          })
        }, 2000)
        //fetch 数据
      } else {
        let type = this.editTypeData
        let len = this.typeList.length
        if (!type.label) {
          this.$message.error('请填写巡检选项')
          return false
        }
        let newType = Object.assign(this.editTypeData, { prop: `ins${len}` })
        this.typeList = [...this.typeList, newType]

        setTimeout(() => {
          this.editDialog = false
          this.$message({
            message: '恭喜你，添加成功',
            type: 'success'
          })
        }, 2000)
      }
    },
    openEditDialog(index, row) {
      this.editDialogType = 1
      this.dialogIndex = index
      this.editTypeData = row
      this.editDialog = true
    },
    removeType() {
      this.removeDialog = false
      this.typeList.splice(this.dialogIndex, 1)
    },
    openRemoveDialog(index, row) {
      this.dialogIndex = index
      this.dialogText = row.label
      this.removeDialog = true
    }
  }
}
</script>



