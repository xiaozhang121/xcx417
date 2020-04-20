<template>
	<view class="">
		
		<form bindsubmit="formSubmit">
		
		   <view class="input-area">
		
		      <view class="input-log">  
		
		        <image class="userinfo-logIcon" src="{{logIcon}}"></image>  
		
		        <input id="username" name="username" maxlength='4' type="text" placeholder="姓名" />
		
		      </view>
		
		      <view class="input-log">
		
		        <image class="userinfo-logIcon" src="{{pwdIcon}}"></image>  
		
		        <input id="password" name="password" type="number" maxlength="11" placeholder="手机号" />
		
		      </view>
		
		    </view>
		
		    <view class="btn-area">
		
		        <button open-type="getUserInfo" lang="zh_CN" bindgetuserinfo="onGotUserInfo"  disabled="{{disabled}}" style="background-color:{{loginBtnBgBgColor}}"  formType="submit"  loading="{{btnLoading}}"> {{loginBtnTxt}} </button>
		
		    </view>
		
		</form>
	</view>
</template>

<script>
</script>

<style>
</style>
