<template>
  <div>
    <el-table
      row-key="order"
      ref="table"
      border
      :data="tableData"
      style="width: 100%"
    >
      <el-table-column
        label="值班时间"
        width="150"
        align='center'
      >
        <el-table-column
          prop='order'
          label='组 \ 岗位'
          align='center'
        ></el-table-column>
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
      <TableColumn
        v-for='timeItem in timeLimitList'
        :key="timeItem.timer"
        @visi-handler='visiHandler'
        @remove-handler='removeHandler'
        :tiemTypeOrder='timeItem.timer'
        :options='options'
        timeLimit='0:00-8:30'
      ></TableColumn>

      <el-table-column
        label='休息'
        align='center'
      >
        <template slot-scope="scope">
          <el-select
            v-model="scope.row.rest"
            multiple
            placeholder="请选择"
            filterable
          >
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </template>
      </el-table-column>
      <el-table-column
        label='操作'
        align='center'
      >
        <template
          slot-scope="scope"
          v-if='tableLen-1 === scope.$index'
        >
          <el-button
            size="mini"
            @click="handlerAdd(scope.$index, scope.row)"
          >增加</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-row
      style="margin-top:30px"
      type="flex"
      justify="end"
    >
      <el-date-picker
        format="yyyy 年 MM 月"
        value-format="yyyy-MM"
        v-model="yearAndMonth"
        type="month"
        placeholder="选择月"
      >
      </el-date-picker>
      <el-button
        style="margin-left:30px"
        type='primary'
        @click='initTableListHandler'
      >生成值班表</el-button>
    </el-row>

  </div>
</template>

<script>
import Sortable from "sortablejs";
import TableColumn from "./tableColumn";

const originOptions = [
  {
    value: "01",
    label: "朱"
  },
  {
    value: "02",
    label: "争"
  },
  {
    value: "03",
    label: "杉"
  },
  {
    value: "04",
    label: "伟"
  },
  {
    value: "05",
    label: "培"
  },
  {
    value: "06",
    label: "谢"
  },
  {
    value: "07",
    label: "路"
  },
  {
    value: "08",
    label: "峰"
  },
  {
    value: "09",
    label: "雷"
  },
  {
    value: "10",
    label: "涛"
  }
];

export default {
  components: {
    TableColumn
  },
  data() {
    return {
      prevMonthRestDay: 3,
      yearAndMonth: "",
      timeLimitList: [
        //三个时间阶段
        {
          timer: 1,
          value: "0:00-8:30"
        },
        {
          timer: 2,
          value: "8:30-18:00"
        },
        {
          timer: 3,
          value: "18:00-0:00"
        }
      ],
      options: originOptions,
      tableData: [
        {
          order: 1,
          one1: [],
          one2: [],
          one3: [],
          two1: [],
          two2: [],
          two3: [],
          three1: [],
          three2: [],
          three3: [],
          rest: []
        }
      ]
    };
  },
  computed: {
    tableLen: function() {
      return this.tableData.length;
    }
  },
  watch: {
    tableLen: function() {
      this.options = originOptions;
      console.log("11");
    }
  },
  mounted() {
    const table = document.querySelector(".el-table__body-wrapper tbody");
    const self = this;
    Sortable.create(table, {
      onEnd({ newIndex, oldIndex }) {
        const targetRow = self.tableData.splice(oldIndex, 1)[0];
        self.tableData.splice(newIndex, 0, targetRow);
      }
    });
  },
  methods: {
    removeHandler() {
      this.options = originOptions;
    },
    visiHandler(isShow) {
      if (!isShow) {
        this.options = this.removeSelected();
      }
    },
    removeSelected() {
      let data = this.tableData[this.tableLen - 1];

      let selectedData = [
        ...data.one1,
        ...data.one2,
        ...data.one3,
        ...data.two1,
        ...data.two2,
        ...data.two3,
        ...data.three1,
        ...data.three2,
        ...data.three3,
        ...data.rest
      ];
      let options = this.options;
      for (let i = 0; i < selectedData.length; i++) {
        let selectedVal = selectedData[i];
        options = options.filter(item => {
          return item.value !== selectedVal;
        });
      }

      return options;
    },
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
      } = data;
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
        return false;
      } else {
        return true;
      }
    },
    handlerAdd(index, row) {
      console.log(index, row);
      let isAdd = this.isCanAdd(row);
      if (!isAdd) {
        this.$message.error("请填写完整信息");
        return;
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
        rest: []
      };
      this.tableData = [...this.tableData, newRow];
    },

    //生成值班列表
    initTableListHandler() {
      this.initTableList();
    },
    //获取年月
    getYearAndMonth() {
      let data = this.yearAndMonth;
      return data.split("-");
    },
    //获取下个月
    getNextMonth() {
      let date = this.yearAndMonth;
      let [year, month] = date.split("-");
      month++;
      if (month > 12) {
        year++;
        month %= 12;
      }
      return [year, month];
    },
    //获取某月有多少天
    getCurrentDays(year, month) {
      return new Date(year, month, 0).getDate();
    },
    getFirstDay(year, month) {
      month = parseInt(month) - 1;
      return new Date(year, month, 1).getDay();
    },
    initDateList(year, month) {
      let days = this.getCurrentDays(year, month);
      let firstWeek = this.getFirstDay(year, month);
      let weekList = ["日", "一", "二", "三", "四", "五", "六"];
      let dateList = [];
      for (let i = 1; i <= days; i++) {
        let weekIndex = (firstWeek + i - 1) % 7;
        let day = `${this.yearAndMonth}-${i}`;
        dateList.push({
          day,
          week: weekList[weekIndex]
        });
      }
      return dateList;
    },
    //nextMonth 多余列表
    initNextMonthList(list) {
      let [year, month] = this.getNextMonth();
      let weekList = this.initDateList(year, month);
      let len = list.length;
      let nextList = [];
      if (list && list.length) {
        for (let index in list) {
          let item = list[index];
          item = Object.assign({}, item, weekList[index]);
          nextList.push(item);
        }
      }
      return nextList;
    },
    //生成值班列表
    initTableList() {
      if (!this.yearAndMonth) {
        this.$message.error("请选择日期");
        return;
      }
      let tableLen = this.tableLen;
      let [year, month] = this.getYearAndMonth();
      let weekList = this.initDateList(year, month);
      let maxDay = this.getCurrentDays(year, month);
      maxDay = maxDay - this.prevMonthRestDay;
      let forLen = parseInt(maxDay / tableLen); //循环次数
      let restLen = parseInt(maxDay % tableLen); //余数量

      this.forTable(forLen, restLen, weekList);
    },
    forTable(forLen, restLen, weekList) {
      let arr = [...this.tableData];
      let data = [];
      for (let i = 0; i < forLen; i++) {
        data.push(...arr);
      }
      data.push(...arr.slice(0, restLen));
      let tableList = [];
      let prevMonthRestDay = this.prevMonthRestDay;
      console.log(data.length);
      for (let i = 0; i < data.length; i++) {
        let item = Object.assign({}, data[i], weekList[i + prevMonthRestDay]);
        tableList.push(item);
      }

      let nextMonthList = [];
      let nextMonthLen = null;
      if (restLen === 0) {
        nextMonthList = [];
        nextMonthLen = 0;
      } else {
        nextMonthLen = this.tableLen - restLen;
        nextMonthList = arr.slice(-nextMonthLen);
      }

      // console.log('------------------------------------')
      // console.log(tableList, nextMonthList, nextMonthLen)
      // console.log('------------------------------------')
      nextMonthList = this.initNextMonthList(nextMonthList);
      console.table(tableList);
      this.tbList = tableList;
    }
  }
};
</script>