<template>
  <div class="app flex-row align-items-center">
    <div class="container">
      <b-row class="justify-content-center">
        <b-col md="8">
          <b-card-group>
            <b-card no-body class="p-4">
              <b-card-body>
                <b-form>
                  <h1>一剑管理后台</h1>
                  <p class="text-muted">登录到您的账户</p>
                  <b-input-group class="mb-3">
                    <b-input-group-prepend><b-input-group-text><i class="icon-user"></i></b-input-group-text></b-input-group-prepend>
                    <b-form-input  v-model.trim="username" v-validator.required="{ title: '用户名' }" type="text" class="form-control" placeholder="用户名" autocomplete="username email" />
                  </b-input-group>
                  <b-input-group class="mb-4">
                    <b-input-group-prepend><b-input-group-text><i class="icon-lock"></i></b-input-group-text></b-input-group-prepend>
                    <b-form-input type="password" v-model.trim="password" id="password" v-validator.required="{ title: '密码' }"  class="form-control" placeholder="Password" autocomplete="current-password" />
                  </b-input-group>
                  <b-row>
                    <b-col cols="6">
                      <b-button variant="primary" @click="submit" class="px-4">登录</b-button>
                    </b-col>
                    <b-col cols="6" class="text-right">
                      <b-button variant="link" class="px-0">忘记密码?</b-button>
                    </b-col>
                  </b-row>
                </b-form>
              </b-card-body>
            </b-card>
            <b-card no-body class="text-white bg-primary py-5 d-md-down-none" style="width:44%">
              <b-card-body class="text-center">
                <div>
                  <h2>注册</h2>
                  <p>注册一剑科技管理后台</p>
                  <b-button variant="primary" class="active mt-3">马上注册!</b-button>
                </div>
              </b-card-body>
            </b-card>
          </b-card-group>
        </b-col>
      </b-row>
    </div>
  </div>
</template>

<script>
    import ls from '@/utils/localStorage'
    export default {
        name: 'Login',
        data() {
            return {
                username: '', // 用户名
                password: '', // 密码
                msg: '', // 消息
                msgType: '', // 消息类型
                msgShow: false // 是否显示消息，默认不显示
            }
        },
        methods: {
            submit() {

                const user = {
                    name: this.username,
                    password: this.password
                }
                const localUser = this.$store.state.user

                if (localUser) {
                    if (localUser.name !== user.name || localUser.password !== user.password) {
                        this.showMsg('用户名或密码不正确')
                    } else {
                        this.$store.dispatch('login')
                    }
                } else {
                    this.showMsg('不存在该用户')
                }

            },
            showMsg(msg, type = 'warning') {
                this.msg = msg
                this.msgType = type
                this.msgShow = false

                this.$nextTick(() => {
                    this.msgShow = true
                })
            }
        }
    }
</script>
