<template>
    <div class="flex flex-col items-center w-full max-w-xl px-10 pb-10 mx-3 mb-10 text-gray-600 bg-white rounded-lg shadow-lg">
      <h1 class="text-center header-style">Account Preferences</h1>
      <alert-item :type="alertType" :message="alertMessage" @clear-alert="clearAlert" />
      <div class="w-full mb-5 border-b">
        <p class="text-lg font-semibold text-teal-600">Name:</p>
        <input-item :text="fullName" type="name" :busy="busy" @status-change="busy = !busy" @alert-event="setAlert" />
      </div>
      <div class="w-full mb-5 border-b font">
        <p class="text-lg font-semibold text-teal-600 ">Email:</p>
        <input-item :text="user['email']" type="email" :busy="busy" @status-change="busy = !busy" @alert-event="setAlert" />
      </div>
      <div class="w-full border-b">
        <p class="font-semibold text-teal-600 lg inline">Password:</p>
        <password-item text="**********" :busy="busy" @status-change="busy = !busy" @alert-event="setAlert" />
      </div>
    </div>
</template>

<script>
import { mapState } from 'vuex';
import InputItem from '@/views/Settings/InputItem.vue';
import PasswordItem from '@/views/Settings/PasswordItem.vue';
import AlertItem from '@/components/AlertItem.vue';

export default {
  name: 'Preferences',
  components: { 'input-item': InputItem, 'password-item': PasswordItem, 'alert-item': AlertItem },
  data() {
    return {
      busy: false,
      alertType: '',
      alertMessage: '',
    };
  },
  computed: {
    ...mapState({
      user: (state) => state.account.user,
    }),
    fullName: function() {
      return this.user['first_name'] + ' ' + this.user['last_name'];
    },
  },
  methods: {
    setAlert(e) {
      this.alertType = e['type'];
      this.alertMessage = e['message'];
    },
    clearAlert() {
      this.alertType = '';
      this.alertMessage = '';
    },
  },
};
</script>
