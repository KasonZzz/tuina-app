<template>
	<view>
		<view class="uni-common-mt">
			<view class="">
				<view class="box">
					<view class="boxTitle">标题</view>
					<view class="uni-textarea textarea">
						<textarea  auto-height />
						</view>
				</view>

				<view class="box">
					<view class="boxTitle">描述</view>
					<view class="uni-textarea textarea" >
						<textarea  auto-height />
					</view>
				</view>
				
				<view class="box">
					<view class="boxTitle">价格</view>
					<view class="price">
						<input class="price" type="number" placeholder="这是一个数字输入框" />
					</view>
						
				</view>
				
				<view class="box">
					
					<picker @change="bindPickerChange" :value="index" :range="array">
						<view class="boxTitle">类别</view>
						<view class="picker">{{array[index]}}</view>
					</picker>
				</view>
			</view>
			
			
			
			<view class="ImgBox">
				<view class="uni-uploader">
					<view class="uni-uploader-head">
						<view class="uni-uploader-title">点击可预览选好的图片</view>
						<view class="uni-uploader-info">{{imageList.length}}/{{maxImgLength}}</view>
					</view>
					<view class="uni-uploader-body">
						<view class="uni-uploader__files">
							<block v-for="(image,index) in imageList" :key="index">
								<view class="uni-uploader__file">
									<image class="uni-uploader__img" :src="image" :data-src="image" @tap="previewImage" mode="aspectFill"></image>
								</view>
							</block>
							<view class="uni-uploader__input-box">
								<view class="uni-uploader__input" @tap="chooseImage">
									<!-- <image src="../../../static/images/0.jpg" class="w-100"></image> -->
								</view>
							</view>
						</view>
					</view>
				</view> 
			</view> 
		</view>
		<view class="uni-center">
			<button @click="uploadImg()" type="primary" class="submit">确认发布</button>
		</view>
	</view>
</template>
<script>
	import permision from "@/components/common/permission.js"
	
	var sourceType = [
		['camera'],
		['album'],
		['camera', 'album']
	]
	var sizeType = [
		['compressed'],
		['original'],
		['compressed', 'original']
	]
	export default {
		data() {
			return {
				index: 0,
				imageList: [], // 图片集合用于回显页面和上传文件
				sourceTypeIndex: 2,
				sourceType: ['拍照', '相册', '拍照或相册'],
				sizeTypeIndex: 2,
				sizeType: ['压缩', '原图', '压缩或原图'],
				countIndex: 3,
				maxImgLength: 5, //最大图片数，从需要页面加载的时候从用户信息中拿取
				imgs: {}, //键值对图片  上传的时候应
				array: ['中国', '美国', '巴西', '日本']
			}
		},
		onUnload() {},
		methods: {
			// 选择图片
			chooseImage: async function() {
				// 如果图片大于我设置的最大图片数
				if (this.imageList.length >= this.maxImgLength) {
					// 判断是否需要清空相册
					let isContinue = await this.isFullImg();
					if (!isContinue) {
						return;
					}
				}
				// #ifdef APP-PLUS
				//选择相机或相册时 需要弹出actionsheet，目前无法获得是相机还是相册，在失败回调中处理
				if (this.sourceTypeIndex !== 2) {
					let status = await this.checkPermission();
					if (status !== 1) {
						return;
					}
				}
				// #endif
				if (this.imageList.length === this.maxImgLength || this.imageList.length > this.maxImgLength) {
					let isContinue = await this.isFullImg();
					if (!isContinue) {
						return;
					}
				}
				// uniapp的选择图组建
				uni.chooseImage({
					// 判断imageList是否超过最大值
					count: this.maxImgLength - this.imageList.length,
					success: (res) => {
						// 将图片路径回显
						this.imageList = this.imageList.concat(res.tempFilePaths);
						// 拿到键值对的图片 主要用于下方上传
						this.imgs = this.imageList.map((value, index) => {
							return {
								name: "file" + index,
								uri: value
							}
						})
					},
					fail: (err) => {
						// #ifdef APP-PLUS
						if (err['code'] && err.code !== 0 && this.sourceTypeIndex === 2) {
							this.checkPermission(err.code);
						}
						// #endif
						// #ifdef MP
						uni.getSetting({
							success: (res) => {
								let authStatus = false;
								switch (this.sourceTypeIndex) {
									case 0:
										authStatus = res.authSetting['scope.camera'];
										break;
									case 1:
										authStatus = res.authSetting['scope.album'];
										break;
									case 2:
										authStatus = res.authSetting['scope.album'] && res.authSetting['scope.camera'];
										break;
									default:
										break;
								}
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相机或相册获取图片，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						})
						// #endif
					}
				})
			},
			// 上传方法
			uploadImg: function() {
				// 显示LOADING
				uni.showLoading({
					title: '上传中'
				});
				// 判断图片是否为空
				if (JSON.stringify(this.imgs) === "{}") {
					uni.hideLoading()
					uni.showToast({
						title: "请选择图片",
						icon: "none",
						position: "center"
					})
				}
				uni.uploadFile({
					url: 'http://192.168.0.105:8080/common/file', //仅为示例，非真实的接口地址
					files: this.imgs,
					formData: {
						'count': this.maxImgLength
					},
					success: (res) => {
						this.pageEmpty();
						setTimeout(function() {
							uni.hideLoading()
							uni.showToast({
								title: "上传成功"
							})
						}, 1000)
					}
				});
			},
			//判断图片是否超过用户可上传的最大限度
			isFullImg: function() {
				return new Promise((res) => {
					uni.showModal({
						content: "已经有" + this.maxImgLength + "张图片了,是否清空现有图片？",
						success: (e) => {
							if (e.confirm) {
								this.imageList = [];
								res(true);
							} else {
								res(false)
							}
						},
						fail: () => {
							res(false)
						}
					})
				})
			},
			//预览图片
			previewImage: function(e) {
				var current = e.target.dataset.src
				uni.previewImage({
					current: current,
					urls: this.imageList
				})
			},
			pageEmpty: function() {
				this.imageList = [];
			},
			bindPickerChange: function(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
			},
			// 检查权限是否开启
			async checkPermission(code) {
				let type = code ? code - 1 : this.sourceTypeIndex;
				let status = permision.isIOS ? await permision.requestIOS(sourceType[type][0]) :
					await permision.requestAndroid(type === 0 ? 'android.permission.CAMERA' :
						'android.permission.READ_EXTERNAL_STORAGE');
				if (status === null || status === 1) {
					status = 1;
				} else {
					uni.showModal({
						content: "没有开启权限",
						confirmText: "设置",
						success: function(res) {
							if (res.confirm) {
								permision.gotoAppSetting();
							}
						}
					})
				}
				return status;
			}
		}
	}
</script>

<style>
	@import "../../../static/styles/uni.css";
	.center{
		text-align: center;
	}
	.cell-pd {
		padding: 22rpx 30rpx;
	}

	.list-pd {
		margin-top: 50rpx;
	}

	.ImgBox {
		text-align: center;
	}
	

	.ImgBox .uni-uploader {
		margin: 30rpx;
		padding: 20rpx;
		display: inline-block;
		width: 700rpx;
		height: auto;
		color: #00000;
		border-radius: 36rpx;
		background: #eaebec;
	}
	
	.box{
		margin: 25rpx;
		width: 700rpx;
		border-radius: 36rpx;
		background: #eaebec;
		display:inline-block;
	}
	.boxTitle{
		display: inline-block;
		margin: 25rpx;
		color: #00000;
		font-size: 34rpx;
		line-height: 30rpx;
		letter-spacing: 10rpx;
		text-align: left;
	}
	
	.submit{
		margin: 80rpx;
		width: 600rpx;
		height: 100rpx;
		border-radius: 36rpx;
		background: #dba871;
		color: #FFF9FF;
		font-size: 35rpx;
		letter-spacing: 30rpx;
	}
	.textarea{
		margin-left: 10rpx;
		background: none;
		color: #DADADA;
		text-align: left;
	}
	.picker{
		width: 200rpx;
		color: #DADADA;
		display: inline-block;
	}
	.price{
		width: 500rpx;
		color: #00000;
		display: inline-block;
	}
	
</style>
