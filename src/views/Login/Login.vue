<template>
  <div class="login">
    <div class="loginPanel">
      <el-form label-position="left" label-width="60px" :model="formLabelAlign">
        <el-form-item label="账号">
          <el-input v-model="formLabelAlign.account"></el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input show-password v-model="formLabelAlign.password"></el-input>
        </el-form-item>
        <el-form-item label="验证码" class="validateBox">
          <el-row>
            <el-col :span="12"
              ><el-input v-model="formLabelAlign.validateCode"></el-input
            ></el-col>
            <el-col :span="12"
              ><div style="border: none" @click="refreshCode">
                <HIdentify :identifyCode="identifyCode"></HIdentify></div
            ></el-col>
          </el-row>
        </el-form-item>
      </el-form>
      <el-button type="success" style="width: 100%">登录</el-button>
    </div>
  </div>
</template>

<script>
import { HIdentify } from "@/components/index";
export default {
  name: "Login",
  components: {
    HIdentify,
  },
  data() {
    return {
      // 登录的相关数据
      formLabelAlign: {
        account: "",
        password: "",
        validateCode: "",
      },
      // 可选值
      identifyCodes: "1234567890",
      identifyCode: "",
    };
  },
  methods: {
    randomNum(min, max) {
      return Math.floor(Math.random() * (max - min) + min);
    },
    refreshCode() {
      this.identifyCode = "";
      this.makeCode(this.identifyCodes, 4);
      console.log(this.identifyCode);
    },
    // 生成随机数
    makeCode(o, l) {
      for (let i = 0; i < l; i++) {
        this.identifyCode +=
          this.identifyCodes[this.randomNum(0, this.identifyCodes.length)];
      }
    },
  },
  mounted() {
    const self = this;
    self.makeCode(this.identifyCodes, 4);
    this.refreshCode();
  },
};
</script>

<style scoped>
.login {
  display: flex;
  justify-content: space-around;
}
.loginPanel {
  width: 30%;
  margin-top: 80px;
  padding: 30px;
  background-color: rgb(243, 242, 236);
}
</style>
