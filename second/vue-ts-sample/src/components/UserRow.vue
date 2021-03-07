<template>
  <tr>
    <td>
      <span v-show="!editable" @click="edit">{{ user.nickname }}</span>
      <input
        v-model="user.nickname"
        v-if="editable"
        @blur="editable = false"
        ref="editNickname"
      />
    </td>
  </tr>
</template>

<script>
import Vue from "vue";

export function User(nickname, email) {
  this.nickname = nickname;
  this.email = email;
}

export default Vue.extend({
  props: {
    user: {
      type: User,
      required: true,
    },
  },
  data() {
    return {
      editable: false,
    };
  },
  methods: {
    edit() {
      this.editable = true;
      this.$nextTick(() => {
        this.$refs.editNickname.focus();
      });
    },
  },
});
</script>

<style module>
td input {
  width: 95%;
}
</style>