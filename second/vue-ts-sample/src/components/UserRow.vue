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
import { defineComponent, ref, nextTick } from "@vue/composition-api";

// vue3.0
export default defineComponent({
  props: {
    user: {
      type: Object,
      required: true,
    },
  },
  setup() {
    const editable = ref(false);
    const editNickname = ref(null);

    // methodsの変わり
    const edit = () => {
      editable.value = true;
      nextTick(() => {
        editNickname.value.focus();
      });
    };

    return {
      editable,
      edit,
      editNickname,
    };
  },
});

// vue 2.0
// export default Vue.extend({
//   props: {
//     user: {
//       type: User,
//       required: true,
//     },
//   },
//   data() {
//     return {
//       editable: false,
//     };
//   },
//   methods: {
//     edit() {
//       this.editable = true;
//       this.$nextTick(() => {
//         this.$refs.editNickname.focus();
//       });
//     },
//   },
// });
</script>

<style module>
td input {
  width: 95%;
}
</style>