<template>
	<div class='home'>
		<map id="myMap" style="width: 100%; height: 300px;" :latitude="latitude" 
			:longitude="longitude" show-location></map>
		<u-tabs name="cate_name" count="cate_count" :list="list" :is-scroll="false" bar-height="6" bar-width="80"
			:current="current" active-color="#F0D208" @change="change">
		</u-tabs>
		<div class="formBox">
			<div v-if='current==0'>
				<u-form :model="form">
					<u-form-item label="姓名" prop="name">
						<u-input v-model="form.name" />
					</u-form-item>
					<u-form-item label="简介" prop="intro">
						<u-input v-model="form.intro" />
					</u-form-item>
				</u-form>
			</div>
			<div v-if='current==1'>
				222222222222
			</div>
		</div>

	</div>
</template>

<script>
	export default {

		data() {
			return {
				mapCtx: '',
				latitude: '',
				longitude: '',
				list: [{
					cate_name: '定位洗车'
				}, {
					cate_name: '智能柜洗车'
				}],
				current: 0,
				form: {
					name: '',
					intro: ''
				},
				rules: {
					name: [{
						required: true,
						message: '请输入姓名',
						// 可以单个或者同时写两个触发验证方式
						trigger: 'blur,change'
					}],
					intro: [{
						min: 5,
						message: '简介不能少于5个字',
						trigger: 'change'
					}]
				}
			}
		},
		created() {
			this.mapCtx = wx.createMapContext('myMap')
			const that = this
			wx.getLocation({
				type: 'gcj02',
				success(res) {
					console.log(res)
					that.latitude = res.latitude
					that.longitude = res.longitude
				}
			})
		},
		methods: {
			// tabs点击
			change(index) {
				this.current = index;
			},
			// 地图拖动事件
			// getRegionChange: function(res) {
			// 	var that = this;
			// 	// 改变中心点位置  
			// 	console.log(res)
			// 	if (res.type == "end") {
			// 		that.getCenterLocation();
			// 	}
			// },
			/** * 得到中心点坐标 */
			// getCenterLocation: function() {
			// 	var that = this;
			// 	this.mapCtx.getCenterLocation({
			// 		success: function(res) {
			// 			console.log('getCenterLocation----------------------->');
			// 			console.log(res);
			// 			that.updateCenterLocation(res.latitude, res.longitude);
			// 			that.regeocodingAddress();
			// 			that.queryMarkerInfo();
			// 		}
			// 	})
			// 	}
			}
		}
</script>

<style lang="scss">
	.home {
		display: flex;
		justify-content: center;
		flex-wrap: wrap;

		.u-tabs {
			width: 500rpx;

			/deep/ .u-tab-item {
				color: #F0D208 !important;
				font-size: 16px !important;
			}

		}

		.formBox {
			width: 450rpx;
		}
	}
</style>
