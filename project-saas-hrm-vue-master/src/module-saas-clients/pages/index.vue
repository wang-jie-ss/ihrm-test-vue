<template>
  <div class="dashboard-container">
    <div class="app-container"> 
      <el-card shadow="never">
        <el-table :data="dataList" border style="width: 100%">
            <!-- prop : 表示的是数组中每个元素对象的属性名 -->
            <el-table-column fixed type="index" label="序号" width="50"></el-table-column>
            <el-table-column fixed prop="name" label="企业名称"  width="200"></el-table-column>
            <el-table-column fixed prop="version" label="版本"  width="150"></el-table-column>
            <el-table-column fixed prop="companyPhone" label="联系电话"  width="150"></el-table-column>
            <el-table-column fixed prop="expirationDate" label="截至时间"  width="150"></el-table-column>
            <el-table-column fixed prop="state" label="状态"  width="150">
              <template slot-scope="scope">
                <!-- 开关组件
                    active-value: 激活的数据值
                    active-color: 激活的颜色
                    inactive-value: 未激活
                    inactive-color:未激活的颜色
                -->
                 <el-switch 
                    v-model="scope.row.state" 
                    inactive-value="0"
                    active-value="1"
                    disabled
                    active-color="#13ce66" 
                    inactive-color="#ff4949">
                 </el-switch> 
              </template>
            </el-table-column>
            <el-table-column fixed ="right" label="操作"  width="150">
              <template slot-scope="scope">
                <router-link :to="'/saas-clients/details/'+scope.row.id">查看</router-link>
                 <!-- <el-button type="text" size="small">编辑</el-button>  -->
              </template>
            </el-table-column>
            
        </el-table>
      </el-card>
     </div>
  </div>
</template>


<script>
import {list} from '@/api/base/saasClient'
export default {
  name: 'saas-clients-index',
  components: {},
  data(){
    return {
      dataList: []
    }
  },
  methods: {
    getList(){
      //调用api发起请求
      //res=响应数据
      list().then(res =>{
        this.dataList= res.data.data;
      });
    } 
  },
  // 创建完毕状态
  created() {
    this.getList();
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.alert {
  margin: 10px 0px 0px 0px;
}
.pagination {
  margin-top: 10px;
  text-align: right;
}
</style>
