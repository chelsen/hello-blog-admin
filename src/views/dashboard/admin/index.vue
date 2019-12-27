<template>
  <div class="dashboard-editor-container">

    <panel-group :quantity-object="quantityObject" />

    <el-row :gutter="32">
      <el-col :xs="36" :sm="36" :lg="15">
        <div style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
          <line-chart :chart-data="lineChartData" />
        </div>
      </el-col>
      <el-col :xs="36" :sm="36" :lg="9">
        <div class="chart-wrapper">
          <visits-ranking-table />
        </div>
      </el-col>
    </el-row>

    <el-row :gutter="8">
      <el-col :xs="{span: 24}" :sm="{span: 24}" :md="{span: 24}" :lg="{span: 8}" :xl="{span: 8}" style="padding-right:8px;margin-bottom:30px;">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>系统信息</span>
          </div>
          <system-info-table />
        </el-card>
      </el-col>
      <el-col :xs="{span: 24}" :sm="{span: 12}" :md="{span: 12}" :lg="{span: 8}" :xl="{span: 8}" style="margin-bottom:30px;">
        <div class="chart-wrapper">
          <pie-chart />
        </div>
      </el-col>
      <el-col :xs="{span: 24}" :sm="{span: 12}" :md="{span: 12}" :lg="{span: 8}" :xl="{span: 8}" style="margin-bottom:30px;">
        <box-card />
      </el-col>
    </el-row>
    <el-row :gutter="7">
      <el-col :xs="{span: 24}" :sm="{span: 24}" :md="{span: 24}" :lg="{span: 12}" :xl="{span: 12}" style="padding-right:20px;margin-bottom:30px;">
        <byte-blogs-article-list />
      </el-col>
      <el-col :xs="{span: 24}" :sm="{span: 24}" :md="{span: 24}" :lg="{span: 12}" :xl="{span: 12}" style="padding-left:20px;margin-bottom:30px;">
        <ByteBlogsChatList />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import ByteBlogsArticleList from './components/ByteBlogsArticleList'
import ByteBlogsChatList from './components/ByteBlogsChatList'
import { fetchBolgQuantityTotal } from '@/api/dashboard'
import PanelGroup from './components/PanelGroup'
import LineChart from './components/LineChart'
import PieChart from './components/PieChart'
import SystemInfoTable from './components/SystemInfoTable'
import VisitsRankingTable from './components/VisitsRankingTable'
import BoxCard from './components/BoxCard'
const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145]
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  }
}
export default {
  name: 'DashboardAdmin',
  components: {
    ByteBlogsArticleList,
    ByteBlogsChatList,
    PanelGroup,
    LineChart,
    PieChart,
    SystemInfoTable,
    VisitsRankingTable,
    BoxCard
  },
  data() {
    return {
      quantityObject: null,
      lineChartData: lineChartData.newVisitis
    }
  },
  created() {
    this.load()
  },
  methods: {
    load() {
      fetchBolgQuantityTotal().then(response => {
        this.quantityObject = response.model
      })
    }

  }
}
</script>

<style lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;

  .github-corner {
    position: absolute;
    top: 0px;
    border: 0;
    right: 0;
  }

  .chart-wrapper {
    background: #fff;
    padding: 16px 16px 0;
    margin-bottom: 32px;
  }
}
</style>
