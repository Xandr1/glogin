<template>
  <div class="home">
    <div class="home-left"></div>
    <div class="home-right">
      <div v-if="!isSignIn">
        <h2 class="text">Login</h2>
        <p class="text">Welcome back, please login to your account.</p>
        <div class="google-login">
          <img
            src="../assets/google.png"
            alt="Google"
            class="icon"
            width="50"
            @click="clickSignIn"
          />
        </div>
      </div>
      <div v-else>
        <button class="sign-out" @click="clickSignOut">
          sign out
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "GoogleLogin",
  data() {
    return {
      isInit: false,
      isSignIn: false,
    };
  },
  created() {
    let that = this;
    let checkGauthLoad = setInterval(function () {
      that.isInit = that.$gAuth.isInit;
      that.isSignIn = that.$gAuth.isAuthorized;
      if (that.isInit) clearInterval(checkGauthLoad);
    }, 1000);
  },
  methods: {
    clickSignIn() {
      this.$gAuth
        .signIn()
        .then((GoogleUser) => {
          console.log("GoogleUser", GoogleUser);
          console.log("getId", GoogleUser.getId());
          console.log("getBasicProfile", GoogleUser.getBasicProfile());
          console.log("getAuthResponse", GoogleUser.getAuthResponse());
          console.log(
            "getAuthResponse",
            this.$gAuth.GoogleAuth.currentUser.get().getAuthResponse()
          );
          this.isSignIn = this.$gAuth.isAuthorized;
        })
        .catch((error) => {
          console.error(error);
        });
      console.log(this.isInit, this.isSignIn);
    },
    clickSignOut() {
      this.$gAuth
        .signOut()
        .then(() => {
          this.isSignIn = this.$gAuth.isAuthorized;
          console.log("isSignIn", this.$gAuth.isAuthorized);
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>
<style scoped>
.home {
  display: flex;
  margin: auto;
  margin-top: 100px;
  width: 60%;
  height: 400px;
}

.home-left {
  width: 50%;
  background: url("../assets/login.png") center no-repeat;
  background-size: 100%;
  background-color: #eff2f7;
}

.home-right {
  width: 50%;
  background-color: #ffffff;
}

.text {
  text-align: left;
  margin-left: 20px;
}

.google-login {
  width: 50px;
  margin: 50px auto;
}

.sign-out {
  display: block;
  width: 150px;
  height: 50px;
  cursor: pointer;
  background-color: #ffffff;
  margin: 50px auto;
  text-transform: uppercase;
  font-weight: 700;
  border: 2px solid #cdd3e1;
  border-radius: 5px;
}

.icon {
  cursor: pointer;
}

@media only screen and (max-width: 640px) {
  .home-left {
    display: none;
  }

  .home-right {
    width: 100%;
  }
}
</style>
