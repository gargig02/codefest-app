<template>
  <div :class="$style.root">
    <AppBar />
    <main :class="$style.wrapper">
      <div :class="$style.authContainer">
        <TabLayout :tabs="tabs" @onToggleTab="onToggleTab">
          <div :class="$style.formContainer" slot="login">
            <BarLoader
              :loading="loading"
              color="#E47718"
              :height="10"
              :class="$style.loader"
            />
            <form @submit.prevent="emailLogin">
              <div :class="$style.fieldContainer">
                <!---<label for="email" :class="$style.label">E-mail</label>--->
                <ul>
                  <li>
                    <div :class="$style.field">
                      <svg>
                        <defs>
                          <radialGradient id="grad1" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
                          <stop offset="0%" style="stop-color:rgb(7,249,254);stop-opacity:0.1" />
                          <stop offset="100%" style="stop-color:rgb(7,249,254);stop-opacity:0.2" />
                          </radialGradient>
                        </defs>
                        <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad1)"              points="0,32 0,52 200,52 220,32 220,12 20,12" >
                        </polygon>
                        <foreignObject x="0" y="12" width="220" height="40">
                          <input type="email"
                                v-model="email"
                                required
                                placeholder="Email"/>
                        </foreignObject>
                      </svg>
                    </div>
                <!---<br />--->
                <!---<label for="password" :class="$style.label">Password</label>--->
                <!---<span :class="$style.fieldWrapper">--->
                    <div :class="$style.field">
                      <svg>
                        <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad1)" points="0,32 0,52 200,52 220,32 220,12 20,12"></polygon>
                        <foreignObject x="0" y="12" width="220" height="40">
                          <input type="password"
                                v-model="password"
                                id="login__password"
                                pattern=".{6,}"
                                title="Must be greater than 6 letters."
                                required
                                placeholder="Password" />
                        </foreignObject>
                      </svg>
                    </div>
                  <!---<i
                    class="fas"
                    :class="
                      isPasswordVisible('login__password')
                        ? 'fa-eye'
                        : 'fa-eye-slash'
                    "
                    @click="togglePasswordVisibility('login__password')"
                  ></i>--->
                </span>
              </li>

              <li>
                  <svg>
                <line id="line1" stroke="#07F9FE" stroke-width="1" x1="123" y1="6" x2="200" y2="6"></line>
                <circle cx="205" cy="6" r="5" stroke="#07F9FE" stroke-width="1" fill="none"></circle>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad1)" points="40,32 40,52 160,52 180,32 180,12 60,12"></polygon>
              <foreignObject :class="$style.btn" x="60" y="22" width="100" height="20">
                <a href="#"><b>Login</b></a>
              </foreignObject>
                <polyline points="100,60 160,60 188,33 235,33" fill="none" stroke="#07F9FE" stroke-width="1"></polyline>
                <circle cx="240" cy="33" r="5" stroke="#07F9FE" stroke-width="1" fill="none"></circle>  
              </svg>
              </li>

              <li>
              
              <div :class="$style.forgotPasswd">
                <router-link to="/password/reset">Forgot Password?</router-link>
              </div>
              </li>

            </ul>
            </div>
            </form>
            <div :class="$style.social">
              <button @click="googleLogin" :class="$style.socialButton">
                <img src="@assets/social/google.png" />
              </button>
              <button @click="fbLogin" :class="$style.socialButton">
                <img src="@assets/social/facebook.png" />
              </button>
              <button @click="gitHubLogin" :class="$style.socialButton">
                <img :src="githubImageUrl" />
              </button>
            </div>
          </div>





          <div :class="$style.formContainer" slot="register">
            <BarLoader
              :loading="loading"
              color="#E47718"
              :height="10"
              :class="$style.loader"
            />

          <form @submit.prevent="emailRegister">
            <div :class="$style.fieldContainer">
              <ul>
                <li>
        
                  <div :class="$style.field">
                <svg>
                  <defs>
                    <radialGradient id="grad2" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
                    <stop offset="0%" style="stop-color:rgb(7,249,254);stop-opacity:0.1" />
                    <stop offset="100%" style="stop-color:rgb(7,249,254);stop-opacity:0.2" />
                    </radialGradient>
                  </defs>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad2)"              points="0,32 0,52 200,52 220,32 220,12 20,12" >
                </polygon>
                <foreignObject x="0" y="12" width="220" height="40">
                    <input type="text"
                  id="name"
                  name="name"
                  v-model="name"
                  placeholder="Name"
                  required>
                </foreignObject>
                 </svg>
               </div>
                  
              <div :class="$style.field">
                <svg>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad2)" points="0,32 0,52 200,52 220,32 220,12 20,12"></polygon>
              <foreignObject x="0" y="12" width="220" height="40">
                <input type="email"
                  id="email"
                  name="email"
                  v-model="email"
                  placeholder="Email"
                  required>
              </foreignObject>
                </svg>
              </div>
                  
                </li>
                
                <li>
                  
                  <div :class="$style.field">
                <svg>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad2)"            points="0,32 0,52 200,52 220,32 220,12 20,12" />
                <foreignObject x="0" y="12" width="220" height="40">
                  <input type="password"
                    v-model="password"
                    id="register__password"
                    pattern=".{6,}"
                    title="Must be greater than 6 letters."
                    required
                    placeholder="Password">
                  <!---<i
                    class="fas"
                    :class="
                      isPasswordVisible('register__password')
                        ? 'fa-eye'
                        : 'fa-eye-slash'
                    "
                    @click="togglePasswordVisibility('register__password')"
                  ></i>--->
                </foreignObject>
                 </svg>
               </div>
                  
              <div :class="$style.field">
                <svg>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad2)" points="0,32 0,52 200,52 220,32 220,12 20,12"></polygon>
              <foreignObject x="0" y="12" width="220" height="40">
                <input type="text"
                  id="phone"
                  name="phone"
                  v-model="Phone"
                  placeholder="Phone">
              </foreignObject>
                </svg>
              </div>
                  </li>
                
                <li>        
                  <div :class="$style.field">
                <svg>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad2)"              points="0,32 0,52 200,52 220,32 220,12 20,12" />
                <foreignObject x="0" y="12" width="220" height="40">
                  <input type="text"
                  id="gender"
                  name="gender"
                  v-model="gender"
                  placeholder="Gender">
                </foreignObject>
                 </svg>
               </div>
                  
              <div :class="$style.field">
                <svg>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad2)" points="0,32 0,52 200,52 220,32 220,12 20,12"></polygon>
              <foreignObject x="0" y="12" width="220" height="40">
                <input type="text"
                  id="country"
                  name="country"
                  v-model="country"
                  placeholder="Country">
              </foreignObject>
                </svg>
              </div>
             </li>
                
                <li>
                  <svg>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad2)" points="0,32 0,52 200,52 220,32 220,12 20,12"></polygon>
              <foreignObject x="0" y="12" width="220" height="40">
                <input type="text"
                  id="xyz"
                  name="xyz"
                  v-model="xyz"
                  placeholder="You are a">
              </foreignObject>
                </svg>
                </li>
                
                <li>
                  <svg>
                <line id="line1" stroke="#07F9FE" stroke-width="1" x1="123" y1="6" x2="200" y2="6"></line>
                <circle cx="205" cy="6" r="5" stroke="#07F9FE" stroke-width="1" fill="none"></circle>
                <polygon stroke="#07F9FE" stroke-width="2" fill="url(#grad2)" points="40,32 40,52 160,52 180,32 180,12 60,12"></polygon>
              <foreignObject :class="$style.btn" x="60" y="22" width="100" height="20">
                <a href="#"><b>Register</b></a>
              </foreignObject>
                <polyline points="100,60 160,60 188,33 235,33" fill="none" stroke="#07F9FE" stroke-width="1"></polyline>
                <circle cx="240" cy="33" r="5" stroke="#07F9FE" stroke-width="1" fill="none"></circle>  
              </svg>
              </li>
            </ul>
            </div>
          </form>




            <!---<form :class="$style.form" @submit.prevent="emailRegister">
              <div :class="$style.fieldContainer">
                <label for="name" :class="$style.label">Name</label>
                <input
                  type="text"
                  id="name"
                  name="name"
                  :class="$style.field"
                  v-model="name"
                  required
                />
                <br />
                <label for="email" :class="$style.label">E-mail</label>
                <input
                  type="email"
                  id="email"
                  name="email"
                  :class="$style.field"
                  v-model="email"
                  required
                />
                <br />
                <label for="password" :class="$style.label">Password</label>
                <span :class="$style.fieldWrapper">
                  <input
                    type="password"
                    :class="$style.field"
                    v-model="password"
                    id="register__password"
                    pattern=".{6,}"
                    title="Must be greater than 6 letters."
                    required
                  />
                  <i
                    class="fas"
                    :class="
                      isPasswordVisible('register__password')
                        ? 'fa-eye'
                        : 'fa-eye-slash'
                    "
                    @click="togglePasswordVisibility('register__password')"
                  ></i>
                </span>
              </div>
              <div :class="$style.btnStyle">
                <button value=">" :class="$style.submit">
                  <i class="fas fa-arrow-circle-right"></i>
                </button>
              </div>
            </form>--->
            <div :class="$style.social">
              <button @click="googleLogin" :class="$style.socialButton">
                <img src="@assets/social/google.png" />
              </button>
              <button @click="fbLogin" :class="$style.socialButton">
                <img src="@assets/social/facebook.png" />
              </button>
              <button @click="gitHubLogin" :class="$style.socialButton">
                <img :src="githubImageUrl" />
              </button>
            </div>
          </div>
        </TabLayout>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script>
import { auth } from "firebase/app";

const AppBar = () => import("@components/Menu/AppBar");
const Footer = () => import("@components/Footer");
const TabLayout = () => import("@components/layouts/TabLayout");
import { BarLoader } from "@saeris/vue-spinners";

export default {
  components: {
    AppBar,
    Footer,
    TabLayout,
    BarLoader,
  },
  data() {
    return {
      name: "",
      email: "",
      password: "",
      phone: "",
      gender: "",
      country: "",
      xyz: "",
      referral: this.$route.query.referral || "",
      tabs: [
        {
          name: "login",
          title: "Login",
        },
        {
          name: "register",
          title: "Register",
        },
      ],
      loading: false,
      __stubbed: 0,
      isLogin: true,
    };
  },
  methods: {
    onToggleTab(tabIndex) {
      if (tabIndex === 0) {
        this.isLogin = true;
      } else {
        this.isLogin = false;
      }
    },
    emailLogin() {
      this.loading = true;
      auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then((result) => {
          this.successfulAuth(result, true);
        })
        .catch((err) => {
          this.loading = false;
          this.$toasted.global.error_post({ message: err.message });
        });
    },
    emailRegister() {
      this.loading = true;
      auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then((result) => {
          this.successfulAuth(result, true);
          result.user
            .sendEmailVerification()
            .then(() =>
              this.$toasted.global.success({
                message: "Verification Link has been sent.",
              })
            )
            .catch((err) => {
              this.$toasted.global.error_post({
                message: err.message,
              });
            });
        })
        .catch((err) => {
          this.loading = false;
          if (err.code === "auth/email-already-in-use") {
            this.emailLogin();
          } else {
            this.$toasted.global.error_post({ message: err.message });
          }
        });
    },
    googleLogin() {
      const provider = new auth.GoogleAuthProvider();
      this.socialLogin(provider);
    },
    fbLogin() {
      const provider = new auth.FacebookAuthProvider();
      this.socialLogin(provider);
    },
    gitHubLogin() {
      const provider = new auth.GithubAuthProvider();
      this.socialLogin(provider);
    },
    socialLogin(provider) {
      this.loading = true;
      auth()
        .signInWithPopup(provider)
        .then((result) => this.successfulAuth(result, false))
        .catch((err) => {
          this.loading = false;
          this.$toasted.global.error_post({ message: err.message });
        });
    },
    successfulAuth(result, byEmail) {
      this.loading = true;
      // const { isNewUser } = result.additionalUserInfo;

      result.user
        .getIdToken(true)
        .then((idToken) => {
          this.tryLoginAndRegister(
            idToken,
            byEmail ? this.name : result.user.displayName,
            byEmail
          );
        })
        .catch((err) => {
          this.loading = false;
          this.$toasted.global.error_post({ message: err.message });
          result.user.delete();
        });
    },
    tryLoginAndRegister(idToken, name, byEmail) {
      this._login(idToken)
        .then((_) => {
          this.loading = false;
          this.onRedirectAuth(false);
        })
        .catch((_) => {
          console.log(_);
          if (byEmail && this.isLogin) {
            this.loading = false;
            this.$toasted.global.error_post({ message: 'No such account exists, register first.' });
          } else {
            this.$recaptcha("login")
              .then((recaptchaToken) => {
                return this._register(idToken, name, this.referral, recaptchaToken);
              })
              .then((_) => {
                this.loading = false;
                this.onRedirectAuth(true);
              })
              .catch((err) => {
                this.loading = false;
                this.$toasted.global.error_post({ message: err.message });
              });
          }
        });
    },
    _login(idToken) {
      return this.$store.dispatch("login", { idToken });
    },
    _register(idToken, name, referralCode, recaptchaToken) {
      return this.$store.dispatch("register", {
        idToken,
        name,
        referralCode,
        recaptchaToken,
      });
    },
    onRedirectAuth(isRegistered) {
      const path =
        this.$route.query.redirect ||
        (isRegistered ? "/profile/edit" : "/dashboard");
      this.$router.push({ path });
    },
    togglePasswordVisibility(inputId) {
      const inputElem = document.getElementById(inputId);
      inputElem.type = inputElem.type === "password" ? "text" : "password";
      this.$data.__stubbed++;
    },
  },
  computed: {
    isPasswordVisible() {
      this.$data.__stubbed; // To make this computed data reactive.
      return (inputId) => {
        const inputElem = document.getElementById(inputId);
        if (inputElem) return inputElem.type !== "password";
      };
    },
    githubImageUrl() {
      if (this.$store.getters.currentTheme === "dark")
        return "assets/social/github-dark.png";
      else return "assets/social/github-light.png";
    },
  },
};
</script>

<style module lang="stylus">

@require '~@styles/anims';

main {
  background-color: rgb(1,0,13);
}

form{
  position: relative;
  margin: auto;
  border: 1px solid #07F9FE;
  background: radial-gradient(circle, rgba(7, 249, 254, 0.2), rgba(7, 249, 254, 0.1));
}

.fieldContainer{
  postion: relative;
  margin: auto;
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0px;
}

.field{
  display: inline;
  text-align: center;
}
svg {
  width: 250px;
  height: 60px;
}

foreignObject div {
  height: 40px;
  padding: 0px;
  margin: 0px;
  display: inline-block;
}

.btn a {
  color: #07F9FE;
  text-decoration: none;  
}

input {
  margin-top: 10px;
  outline: none;
  border: none;
  background: none;
  text-align: left;
  color: #07F9FE;
  padding-left: 20px;
}

form ::placeholder{
  color: #07F9FE;
  opacity: 1;
}

.authContainer {
  $font-size: 16px;
  font-family: courier, monospace;
  max-width: 600px;
  margin: auto;
  width: 100%;

}

.wrapper {
  padding: 200px 0;
  position: relative;
  top: 0;
  z-index: 1;
  font-family: 'Roboto Slab';
  $font-size: 18px;

}

.root {
  height: 100%;
}

.formContainer {

  background-color: rgb(1,0,13);
}

/* .fieldContainer {
  width: 100%;
  margin-bottom: 20px;
  text-align: right;
} 

.field {
  clear: both;
  height: 30px;
  color: var(--text-color);
  box-shadow: var(--inset-box-shadow);
  border: 0;
  outline: 0;
  max-width: 400px;
  width: 100%;
  $font-size: 16px;
  background-color: var(--background-color);
  border-radius: 5px;
  padding-left: 5px;
  margin-bottom: 20px;
} */

.label {
  float: left;
  color: var(--text-color);
  text-align: left;
  font-family: 'Quicksand';
  font-weight: 600;
  height: 30px;
  width: 100px;
}

.fieldWrapper {
  width: 100%;
  position: relative;

  i {
    top: 0;
    right: 7px;
    position: absolute;
    cursor: pointer;
  }
}

.forgotPasswd {
  width: 100%;
  text-align: left;
  padding-left: 220px;
  font-size: small; 
}


.forgotPasswd a{
  color: #07F9FE;
  text-decoration: none;
}

.btnStyle {
  text-align: center;
}

.submit {
  border: 0;
  background: transparent;
  color: var(--background-color-invert);
  box-shadow: var(--box-shadow);
  border-radius: 100%;
  $font-size: 40px;
  height: 40px;
  width: 40px;
  cursor: pointer;
  text-align: center;

  &:hover {
    color: $vermilion;
  }
}

.social {
  width: 100%;
  max-width: 600px;
  margin: auto;
  text-align: center;
  padding: 5px;
  margin-top: 20px;
  border: 0;
  background-color: var(--background-color);
  box-shadow: var(--icon-shadow);
  width: 60%;
  border-radius: 30px 0;

  .socialButton {
    background-color: Transparent;
    background-repeat: no-repeat;
    border: none;
    cursor: pointer;
    overflow: hidden;
    outline: none;

    img {
      margin: 10px;
      width: 40px;
      height: 40px;
    }
  }
}

@media screen and (max-width: 769px) {
  .wrapper {
    width: 90%;
  }
}
</style>
