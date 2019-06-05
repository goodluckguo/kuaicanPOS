<template>
  <div class="leftnav">
    <ul>
      <li>
        <i class="el-icon-goods"></i>
        <div>收银</div>
      </li>
      <li>
        <i class="el-icon-platform-eleme"></i>
        <div>店铺</div>
      </li>
      <li>
        <i class="el-icon-user-solid"></i>
        <div>会员</div>
      </li>
      <li>
        <i class="el-icon-s-data"></i>
        <div>统计</div>
      </li>
      <li>
        <i class="el-icon-s-tools"></i>
        <div>设置</div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'leftNav',
  data() {
    return {}
  }
}
</script>
<style>
.leftnav {
  color: #fff;
  font-size: 10px;
  height: 100%;
  background-color: #1d8ce0;
  float: left;
  width: 5%;
}
.iconfont {
  font-size: 24px;
}
.leftnav ul {
  padding: 0;
  margin: 0;
}
.leftnav li {
  list-style: none;
  text-align: center;
  border-bottom: 1px solid #20a0ff;
}
.leftnav ul li i {
  font-size: 24px;
}
</style>