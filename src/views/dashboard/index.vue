<template>
  <div class="dashboard-container">
    <div class="dashboard-text">name:{{name}}</div>
    <div class="dashboard-text">roles:<span v-for='role in roles' :key='role'>{{role}}</span></div>
    <div style="height:40px; line-height: 40px;">
    	请选择时间：
    	<span id="text" style="display: inline-block;width: 100px;height: 30px;border: 1px solid #CCCCCC;"></span>
    </div>   
    <div id="map-box"></div>
    <div class="pie-box">
    	<div id="pie-box"></div>
    	<div id="circle-box"></div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
// 引入 ECharts 主模块
var echarts = require('echarts/lib/echarts');
require('echarts/lib/chart/map');
require('echarts/lib/component/tooltip');
require('echarts/lib/component/title');
export default {
  name: 'dashboard',
  computed: {
    ...mapGetters([
      'name',
      'roles'
    ])
  },
  mounted: function(){
		this.test();
		this.mapCharts();
  },
  methods: {
  	test(){
  		laydate.render({
			  elem: '#text',
			  max: 'new Date()',
			  value: new Date(),
			  festival: true,
			  zIndex: 99,
			  theme: '#393D49',
			  calendar: true,
		    choose: function(dates){ //选择好日期的回调		
		        }
		})
  	},
  	mapCharts(){
  		 this.mapchart = echarts.init(document.getElementById("map-box"));
  		 this.piechart = echarts.init(document.getElementById("pie-box"));
  		 this.setOptions();
  	},
  	setOptions(){
  		this.mapchart.setOption({ 			
				title: {
					text: '客流统计',
					subtext: '',
					x: 'left',
					y: 'top',
					textStyle: {
						fontSize: 14,
						color: '#666666',
						fontWeight:'normal'
					},
					subtextStyle: {
						color: '#333'
					}
				},
				tooltip: { //提示框
					trigger: 'item'
				},
				legend: { //左侧图例
					orient: 'vertical',
					x: 'left',
					data: ['', '', '']
				},
				dataRange: {//数据条
					min: 0,
					max: 500,
					text: ['高(省客流总人数)', '低(省客流总人数)'],
					position: 'bottom',
					orient: 'horizontal',
					x: 'left',
					y: 'bottom',
					itemWidth: 15,
					color: ['red', 'orange','#E9967A', 'yellow', '#ccc'],
					calculable: true
				},
				series: [{//地图详情
					name: '详情：',
					type: 'map',
					mapType: 'china',
					zoom: 1.3,
					roam: false,
					itemStyle: {
						normal: {
							borderColor: '#F8F8FF',
							borderWidth: 1,
							areaColor: '#ccc', //地图背景色
							label: {
								show: true,
								textStyle: {
									fontSize: 10,
									color: '#8B4513'
								}
							}
						},
						emphasis: { //滑过时的提示框
							label: {
								show: true
							}
						}
					},
					data: [
						{name: '北京',
						 value: 200
						},
						{name: '天津'},						
						{name: '上海'},							
						{name: '重庆'},							
						{name: '河北'},							
						{name: '河南'},							
						{name: '云南'},							
						{name: '辽宁'},							
						{name: '黑龙江'},							
						{name: '湖南'},							
						{name: '安徽'},							
						{name: '山东'},							
						{name: '新疆'},							
						{name: '江苏'},							
						{name: '浙江'},							
						{name: '江西'},							
						{name: '湖北'},							
						{name: '广西',
						 value: 300
						},
						{name: '甘肃'},							
						{name: '山西'},							
						{name: '内蒙古'},							
						{name: '陕西'},							
						{name: '吉林'},							
						{name: '福建'},							
						{name: '贵州'},							
						{name: '广东'},							
						{name: '青海'},							
						{name: '西藏',
						 value: 240
						},
						{name: '四川'},							
						{name: '宁夏'},							
						{name: '海南'},							
						{name: '台湾'},							
						{name: '香港'},							
						{name: '澳门'}							
					]
				}]
  })
  	}
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
@mixin fontSize{
	font-size: 14px;
	color: #666666;
}
@mixin flex{
	display: -webkit-flex;
	display: flex;
	justify-content: space-around;
	align-items:center;
}
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
#map-box{
	width: 800px;
	height: 500px;
	margin: 15px auto;
	border: 1px solid #CCCCCC;
}
.pie-box{
	@include flex;
}
.pie-box div{
	width: 300px;
	height: 300px;
	border: 1px solid #CCCCCC;
}
</style>
