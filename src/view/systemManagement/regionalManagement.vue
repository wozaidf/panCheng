<template>
  <div class="regionalManagement">
    <!-- 区域搜索 -->
    <div class="regionSearch">
      <span>区域名称：</span>
      <el-input v-model="searchRegionalName" placeholder="请输入区域名称" style="width: 250px; margin-right: 20px;" />
      <el-button type="primary">查询</el-button>
      <el-button type="primary" @click="addRegionalForm">新增</el-button>
    </div>
    <!-- 区域信息列表 -->
    <div class="regionalTable">
      <div class="title">
        <span>区域信息列表：</span>
      </div>
      <el-table stripe :data="regionalDate" style="width: 100%">
        <el-table-column align="center" prop="regionalName" label="区域名称" />
        <el-table-column align="center" prop="regionalDetail" label="区域详细" />
        <el-table-column align="center" prop="regionalStreet" label="所属街道" />
        <el-table-column align="center" label="操作">
          <!-- ????? -->
          <template #default="scope">
            <el-button @click="changeRegionalData(scope.row)" link size="small" type="primary" text>
              修改
            </el-button>
            <el-button @click="deleteRegionalData" link size="small" type="primary" text>
              删除
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <!-- 分割线 -->
    <el-divider style="margin-top: 54vh;" />
    <!-- 分页器 -->
    <div class="regionalPager">
      <el-pagination v-model:current-page="currentPage4" v-model:page-size="pageSize4"
        :page-sizes="[100, 200, 300, 400]" :small="false" :disabled="false" :background="false"
        layout="total, sizes, prev, pager, next, jumper" :total="400" @size-change="handleSizeChange"
        @current-change="handleCurrentChange" />
    </div>
    <!-- 新增、修改弹窗Form -->
    <div>
      <el-dialog v-model="dialogFormVisible" :title="dialogFormTitle" style="width:30%">
        <el-form :model="regionalForm" label-position="right" label-width="100px">
          <el-form-item label="区域名称">
            <el-input v-model="regionalForm.regionalName" autocomplete="off" style="width: 400px;" />
          </el-form-item>
          <el-form-item label="区域详细">
            <el-input v-model="regionalForm.regionalDetail" autocomplete="off" style="width: 400px;" />
          </el-form-item>
          <el-form-item label="所属街道">
            <el-input v-model="regionalForm.regionalStreet" autocomplete="off" style="width: 400px;" />
          </el-form-item>
        </el-form>
        <template #footer>
          <span class="dialog-footer">
            <el-button @click="dialogFormVisible = false">取消</el-button>
            <el-button type="primary" @click="dialogFormVisible = false">
              提交
            </el-button>
          </span>
        </template>
      </el-dialog>
    </div>
  </div>
</template>

<script setup lang="ts" name="regionalManagement">
import { ref, reactive } from 'vue'

// 数据
// let colors = [
//   '247, 162, 20',
//   '254, 230, 100',
//   '153, 221, 226',
//   '211, 110, 197',
//   '150, 227, 161',
//   '238, 206, 112',
//   '116, 220, 187',
//   '116, 148, 218',
//   '216, 117, 146',
//   '245, 196, 156'
// ]

// 区域名称 
let searchRegionalName = ref()
// 区域列表数据
let regionalDate = reactive([
  {
    regionalName: '2016-05-03',
    regionalDetail: 'Tom',
    regionalStreet: 'No. 189, Grove St, Los Angeles',
  },
  {
    regionalName: '2016-05-04',
    regionalDetail: 'Tom',
    regionalStreet: 'No. 189, Grove St, Los Angeles',
  },
  {
    regionalName: '2016-05-05',
    regionalDetail: 'Tom',
    regionalStreet: 'No. 189, Grove St, Los Angeles',
  },

])
// 修改区域信息回调
function changeRegionalData(row: any) {
  dialogFormVisible.value = true
  dialogFormTitle.value = "修改区域信息"
  // regionalForm = row
  Object.assign(regionalForm, row)
}
// 删除区域信息回调
function deleteRegionalData() {

}


// 区域弹窗显示boole值
let dialogFormVisible = ref(false)
// 弹窗的title
let dialogFormTitle = ref("新增区域信息")
// 弹窗区域表格
const regionalForm = reactive({
  regionalName: '',
  regionalDetail: '',
  regionalStreet: ''
})


// 新增区域表单信息
function addRegionalForm() {
  dialogFormVisible.value = true

}



// 分页器数据
const currentPage4 = ref(4)
const pageSize4 = ref(100)
// 分页器方法
const handleSizeChange = (val: number) => {
  console.log(`${val} items per page`)
}
const handleCurrentChange = (val: number) => {
  console.log(`current page: ${val}`)
}

// 方法
// 渐变方法 :cell-style="cellStyle"
// function cellStyle(data: { row: any, column: any, rowIndex: number, columnIndex: number }) {
//   const dataLength = tableData.length           // 数据长度
//   const gradientNum = dataLength + 1            // 渐变数量加1
//   const startOpacity = 0.7                      // 起始透明度
//   const interval = startOpacity / gradientNum   // 计算每行的渐变间隔
//   const opacity1 = startOpacity - data.rowIndex * interval
//   const opacity2 = startOpacity - interval - data.rowIndex * interval
//   const styleObj = {
//     backgroundImage:
//       `linear-gradient(to bottom, rgba(${colors[data.columnIndex]}, 
//          ${opacity1}), rgba(${colors[data.columnIndex]},
//           ${opacity2}))`,
//     border: 'none'
//   }
//   return styleObj
// }
</script>

<style scoped>
.regionSearch {
  display: flex;
  align-items: center;
}

.regionalManagement {
  margin: 10px 0 0 10px;
  height: 80vh;
}

.regionalTable {
  margin-top: 25px;
}


.title {
  background-color: rgb(175, 182, 187);
  width: 100%;
  height: 5vh;
  display: flex;

  span {
    font-size: 16px;
    display: flex;
    align-items: center;
    margin-left: 20px;
  }
}

.dialog-footer button:first-child {
  margin-right: 10px;
}

.regionalPager {
  margin-top: -20px;
  display: flex;
  justify-content: flex-end;
}

.divider {
  width: 1px;
  position: absolute;
  top: 0;
  bottom: 0;
  background-color: #ccc;
}
</style>
