
<template>
  <div class="dataList">
    <!-- 顶部按钮 -->
    <div class="topArea">
      <el-button
        size="small"
        type="primary"
        @click="toInput"
      >上报</el-button>
    </div>
    <!-- 中间区域 -->
    <div class="content">
      <el-table :data="tableData" style="width: 100%">
        <!-- 序号 -->
        <el-table-column type="index" label="序号" align="center" />
        <!-- 国家 -->
        <el-table-column prop="country" label="国家" align="center" />
        <!-- 省 -->
        <el-table-column prop="province" label="省" align="center" />
        <!-- 市 -->
        <el-table-column prop="city" label="市" align="center" />
        <!-- 区 -->
        <el-table-column prop="area" label="区" align="center" />
        <!-- 新增确诊 -->
        <el-table-column prop="confirmed" label="新增确诊" align="center" />
        <!-- 疑似 -->
        <el-table-column prop="suspected" label="疑似" align="center" />
        <!-- 死亡 -->
        <el-table-column prop="dead" label="死亡" align="center" />
        <!-- 治愈 -->
        <el-table-column prop="cure" label="治愈" align="center" />
        <!-- 重症 -->
        <el-table-column prop="severe" label="重症" align="center" />
        <!-- 境外输入 -->
        <el-table-column prop="outside" label="境外输入" align="center" />
        <!-- 上报时间 -->
        <el-table-column label="上报时间" align="center">
          <template slot-scope="scope">
            {{ scope.row.inputTime | fmtDate }}
          </template>
        </el-table-column>
      </el-table>
    </div>

  </div>
</template>

<script>
import { get, post } from '@/utils/request'
export default {
  data() {
    return {
      tableData: []

    }
  },
  created() {
    this.getData()
  },
  methods: {
    // 上报数据
    toInput() {
      this.$router.push({
        path: '/data/input'
      })
    },

    // 获取疫情数据信息
    async getData() {
      const params = {
        page: 1,
        pageSize: 100
      }
      const res = await get('/epidemic/pageQuery', params)
      this.tableData = res.data.list
    }

  }
}
</script>

<style scoped>
</style>
