<template>
  <el-table
      :load="loading"
      :data="tableData"
      tooltip-effect="dark"
      style="width: 100%"
      @selection-change="handleSelectionChange"
  >
    <slot name='column'></slot>
  </el-table>
  <el-pagination
    background
    layout="prev, pager, next"
    :total="total"
    :page-size="pageSize"
    :current-page="currentPage"
    @current-change="changePage"
  />
</template>

<script>
import { onMounted, reactive, toRefs, getCurrentInstance } from 'vue'
import axios from '@/utils/axios'
export default {
  name: 'Table',
  props: {
    action: String
  },
  setup(props) {
    const app = getCurrentInstance()
    const state = reactive({
      loading: false,
      tableData: [], // 数据列表
      total: 0, // 总条数
      currentPage: 1, // 当前页
      pageSize: 10, // 分页大小
      multipleSelection: []
    })
    onMounted(() => {
      getList()
    })

    const getList = () => {
      state.loading = true
      axios.get(props.action, {
        params: {
          pageNumber: state.currentPage,
          pageSize: state.pageSize
        }
      }).then(res => {
        state.tableData = res.list
        state.total = res.totalCount
        state.currentPage = res.currPage
        state.loading = false
        app.ctx.goTop() // 回到顶部
      })
    }

    const handleSelectionChange = (val) => {
      state.multipleSelection = val
    }

    const changePage = (val) => {
      state.currentPage = val
      getList()
    }

    return {
      ...toRefs(state),
      changePage,
      handleSelectionChange,
      getList
    }
  }
}
</script>