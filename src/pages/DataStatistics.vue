<template>
  <div>
    <!-- 中国地图 -->
    <div id="china" v-loading="loading" style="height:600px" />
    <!-- 广西地图 -->
    <div id="guangxi" v-loading="loading" style="height:600px" />
    <!-- 上海地图 -->
    <div id="shanghai" v-loading="loading" style="height:600px" />

  </div>
</template>

<script>
// 因为是第三方接口 所以需要导入axios
import axios from 'axios'
export default {
  data() {
    return {
      // 国内各省市疫情数据
      chinaCovidData: [],

      // 初始化图表
      // 广西疫情数据
      guangxiCovidData: [],
      // 上海疫情数据
      shanghaiCovidData: []
    }
  },
  mounted() {
    // 查询当前国内各省市疫情数据信息
    // axios({
    //   url: "https://api.muxiaoguo.cn/api/epidemic?type=epidemicInfectionData&api_key=6f46fea09e825b0b",
    // }).then((res) => {
    // 根据highmaps的data格式对获取到的数据进行过滤
    // let resultChina = res.data.data.map((item) => {
    //   return {
    //     name: item.provinceShortName,
    //     value: item.currentConfirmedCount,
    //   };
    // });
    // 国内疫情数据
    // this.chinaCovidData = resultChina;
    // 加载中国地图
    this.loadChinaMap()

    // 广西疫情数据
    // let resGuangxi = res.data.data.filter(item => {
    //   return item.provinceName == '广西壮族自治区'
    // })
    // 修改数据格式
    // this.guangxiCovidData = resGuangxi[0].cities.map(item => {
    //   return {
    //     name: item.cityName,
    //     value: item.currentConfirmedCount,
    //   };
    // })
    // console.log(this.guangxiCovidData);

    this.loadGuangxiMap()

    // 上海疫情数据
    // let resshanghai = res.data.data.filter(item =>{
    //   return item.provinceName == '上海市'
    // })
    // 修改数据格式
    // this.shanghaiCovidData = resshanghai[0].cities.map(item => {
    //   return {
    //     name: item.cityName,
    //     value: item.currentConfirmedCount,
    //   };
    // })

    this.loadShanghaiMap()
    // });
    this.loading = false
  },
  methods: {
    // 加载中国地图
    loadChinaMap() {
      // 初始化图表
      var data = [{ 'name': '北京', 'value': 15282 }, { 'name': '天津', 'value': 5291 }, { 'name': '河北', 'value': 4523 }, { 'name': '山西', 'value': 5265 }, { 'name': '内蒙古', 'value': 9042 }, { 'name': '辽宁', 'value': 5270 }, { 'name': '吉林', 'value': 7562 }, { 'name': '黑龙江', 'value': 10520 }, { 'name': '上海', 'value': 6534 }, { 'name': '江苏', 'value': 8563 }, { 'name': '浙江', 'value': 7229 }, { 'name': '安徽', 'value': 5224 }, { 'name': '福建', 'value': 5233 }, { 'name': '江西', 'value': 4623 }, { 'name': '山东', 'value': 9661 }, { 'name': '河南', 'value': 9517 }, { 'name': '湖北', 'value': 3659 }, { 'name': '湖南', 'value': 6163 }, { 'name': '广东', 'value': 15669 }, { 'name': '广西', 'value': 6915 }, { 'name': '海南', 'value': 3569 }, { 'name': '重庆', 'value': 17224 }, { 'name': '四川', 'value': 10594 }, { 'name': '贵州', 'value': 5686 }, { 'name': '云南', 'value': 5666 }, { 'name': '西藏', 'value': 5644 }, { 'name': '陕西', 'value': 5617 }, { 'name': '甘肃', 'value': 9854 }, { 'name': '青海', 'value': 6990 }, { 'name': '宁夏', 'value': 5222 }, { 'name': '新疆', 'value': 5560 }, { 'name': '台湾', 'value': 90547 }, { 'name': '香港', 'value': 56823 }, { 'name': '澳门', 'value': 15602 }, { 'name': '南海诸岛', 'value': 566 }, { 'name': '南海诸岛', 'value': 24 }]
      // 初始化图表
      const map = new Highcharts.Map('china', {
        title: {
          text: '中国地图'
        },
        colorAxis: {
          // 设置每个区间的颜色
          dataClasses: [
            {
              color: '#FFE1B3',
              to: 10
            },
            {
              color: '#FDCFA7',
              from: 10,
              to: 100
            },
            {
              color: '#FBB998',
              from: 100,
              to: 1000
            },
            {
              color: '#FAA68A',
              from: 1000,
              to: 5000
            },
            {
              color: '#F8947D',
              from: 5000,
              to: 10000
            },
            {
              color: '#F57669',
              from: 10000,
              to: 50000
            },
            {
              color: '#F2544E',
              from: 100000
            }
          ]
        },
        series: [
          {
            // 将疫情数据进行赋值
            data: data,
            name: '共有疫情人数',
            mapData: Highcharts.maps['cn/china'],
            joinBy: 'name' // 根据 name 属性进行关联
          }
        ]
      })
    },
    // 加载广西地图
    loadGuangxiMap() {
      // 模拟数据
      var data = [{ 'name': '南宁', 'value': 27 }, { 'name': '柳州', 'value': 43 }, { 'name': '桂林', 'value': 89 }, { 'name': '梧州', 'value': 93 }, { 'name': '北海', 'value': 82 }, { 'name': '防城港', 'value': 32 }, { 'name': '钦州', 'value': 4 }, { 'name': '贵港', 'value': 80 }, { 'name': '玉林', 'value': 48 }, { 'name': '百色', 'value': 28 }, { 'name': '贺州', 'value': 62 }, { 'name': '河池', 'value': 61 }, { 'name': '来宾', 'value': 53 }, { 'name': '崇左', 'value': 76 }]
      // 初始化图表
      var map = new Highcharts.Map('guangxi', {
        title: {
          text: '广西壮族自治区'
        },
        colorAxis: {
          min: 0,
          minColor: '#FFE4B5',
          maxColor: '#F14746'
        },
        series: [
          {
            data: data,
            name: '现有疫情人数',
            mapData: Highcharts.maps['cn/guangxi'],
            joinBy: 'name' // 根据 name 属性进行关联
          }
        ]
      })
    },
    // 加载上海地图
    loadShanghaiMap() {
      // 模拟数据
      var data = [{ 'name': '黄浦区', 'value': 53 }, { 'name': '徐汇区', 'value': 66 }, { 'name': '长宁区', 'value': 93 }, { 'name': '静安区', 'value': 43 }, { 'name': '普陀区', 'value': 57 }, { 'name': '虹口区', 'value': 96 }, { 'name': '杨浦区', 'value': 29 }, { 'name': '闵行区', 'value': 7 }, { 'name': '宝山区', 'value': 100 }, { 'name': '嘉定区', 'value': 34 }, { 'name': '浦东新区', 'value': 12 }, { 'name': '金山区', 'value': 90 }, { 'name': '松江区', 'value': 37 }, { 'name': '青浦区', 'value': 75 }, { 'name': '奉贤区', 'value': 61 }, { 'name': '崇明区', 'value': 78 }]
      // 初始化图表
      // 初始化图表
      var map = new Highcharts.Map('shanghai', {
        title: {
          text: '上海市'
        },
        colorAxis: {
          min: 0,
          minColor: '#FFE4B5',
          maxColor: '#F14746'
        },
        series: [
          {
            data: data,
            name: '现有疫情人数',
            mapData: Highcharts.maps['cn/shanghai'],
            joinBy: 'name' // 根据 name 属性进行关联
          }
        ]
      })
    }
  }
}
</script>

<style scoped>

</style>
