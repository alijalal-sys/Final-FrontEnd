<template>
  <div class="auth-page">
    <b-container>
      <h5 class="auth-logo">
        <i class="fa fa-circle text-gray" />
        Motus App
        <i class="fa fa-circle text-warning" />
      </h5>

      <b-modal
        id="modal-1"
        modal-cancel
        title="<h3 class='text-center'>Login</h3>"
      >
        <p class="my-4">
          <LoginCamera />
        </p>
      </b-modal>
      <Widget
        class="widget-auth mx-auto"
        title="<h3 class='mt-0'>Login to your Web App</h3>"
        custom-header
      >
        <p class="widget-auth-nfo text-center py-3">
          Use your email to sign in.
        </p>
        <form
          class="mt"
          @submit.prevent="login"
        >
          <b-alert
            class="alert-sm"
            variant="danger"
            :show="!!errorMessage"
          >
            {{ errorMessage }}
          </b-alert>
          <div class="form-group">
            <input
              ref="email"
              class="form-control no-border"
              required
              type="email"
              name="email"
              placeholder="Email"
            >
          </div>
          <div class="form-group">
            <input
              ref="password"
              class="form-control no-border"
              required
              type="password"
              name="password"
              placeholder="Password"
            >
          </div>
          <b-button
            type="submit"
            size="sm"
            class="auth-btn mb-3"
            variant="inverse"
          >
            Login
          </b-button>
          <div class="m-auto text-center py-2">
            <a
              @click="() => this.$router.push('reset')"
            >
              forget your password?
            </a>
          </div>
          <p class="widget-auth-info">
            or sign in as
          </p>
          <div class="social-buttons">
            <b-button
              v-b-modal.modal-1
              variant="primary"
              class="social-button mb-2"
            >
              <p class="social-text">
                Basic User
              </p>
            </b-button>
          </div>
        </form>
        <p class="widget-auth-info">
          Don't have an account? <br>
          Sorry for that but you can't register by yourself
        </p>
      </Widget>
    </b-container>
    <footer class="auth-footer">
      2020 &copy; The Fifth Team.
    </footer>
  </div>
</template>

<script>
import Widget from '@/components/Widget/Widget';
import LoginCamera from '@/components/Cameras/LoginCamera';
import { SIGN_IN_ADMIN } from '../../graphql/Mutations'

export default {
  name: 'LoginPage',
  components: { Widget, LoginCamera },
  data() {
    return {
      errorMessage: null,
    };
  },
  created() {},
  methods: {
    login() {
      const email = this.$refs.email.value;
      const password = this.$refs.password.value;

      this.$apollo.mutate({
        mutation: SIGN_IN_ADMIN,
        variables: {
          email,
          password
        }
      })
      .then(({ data }) => {
        console.log('Token: ', data.signInAdmin.token)
        localStorage.setItem('X-auth', data.signInAdmin.token);
        localStorage.setItem('isAdmin', true);
        this.$router.push('/app/dashboard');
      })
      .catch(err => {
        this.errorMessage = 'Please Enter Valid Data'
        console.log(err)
      })
    },
  },
};
</script>