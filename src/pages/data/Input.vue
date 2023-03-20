
<template>
  <div class="dataInputs">
    <!-- 上报表单 -->
    <div class="content" style="width: 70%">
      <el-form
        ref="dataForm"
        :model="dataForm"
        label-width="100px"
        class="demo-ruleForm"
      >
        <!-- 省市区 -->
        <el-form-item label="省市区选择" prop="pca">
          <el-cascader
            v-model="dataForm.pca"
            :props="{ label: 'name', value: 'name' }"
            :options="pca"
          />
        </el-form-item>
        <!-- 国家 -->
        <el-form-item label="国家" prop="country">
          <el-input v-model="dataForm.country" />
        </el-form-item>
        <!-- 确诊 -->
        <el-form-item label="确诊" prop="confirmed">
          <el-input v-model="dataForm.confirmed" />
        </el-form-item>

        <!-- 疑似 -->
        <el-form-item label="疑似" prop="suspected">
          <el-input v-model="dataForm.suspected" />
        </el-form-item>
        <!-- 死亡 -->
        <el-form-item label="死亡" prop="dead">
          <el-input v-model="dataForm.dead" />
        </el-form-item>
        <!-- 治愈 -->
        <el-form-item label="治愈" prop="cure">
          <el-input v-model="dataForm.cure" />
        </el-form-item>
        <!-- 重症 -->
        <el-form-item label="重症" prop="severe">
          <el-input v-model="dataForm.severe" />
        </el-form-item>
        <!-- 境外输入 -->
        <el-form-item label="境外输入" prop="outside">
          <el-input v-model="dataForm.outside" />
        </el-form-item>
      </el-form>
    </div>
    <!-- 提交按钮 -->
    <div class="topArea" style="margin-left: 100px">
      <!-- 新增按钮 -->
      <el-button
        type="primary"
        @click="submitHandler('dataForm')"
      >提交</el-button>
    </div>
  </div>
</template>

<script>
import { get, post } from '@/utils/request'
import pca from '@/assets/pca.json'
export default {
  data() {
    return {
      dataForm: {},

      pca
    }
  },
  methods: {
    // 提交
    submitHandler(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          // alert('submit!');
          // 深拷贝
          const data = { ...this.dataForm }
          data.province = this.dataForm.pca[0]
          data.city = this.dataForm.pca[1]
          data.area = this.dataForm.pca[2]
          delete data.pca
          post('/epidemic/saveOrUpdate', data).then((res) => {
            this.$message({
              type: 'success',
              message: res.message
            })
            this.godataList()
            this.dataForm = {}
          })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    // 跳转到数据列表
    godataList() {
      this.$router.push({
        path: '/data/list'
      })
    }
  }
}
</script>

<style scoped>
</style>
