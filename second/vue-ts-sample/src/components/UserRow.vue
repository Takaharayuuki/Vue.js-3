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

<script lang="ts">
import { defineComponent, ref, nextTick, PropType } from "@vue/composition-api";

// vue3.0

export interface User {
  nickname: string;
  email: string;
}

export default defineComponent({
  props: {
    user: {
      type: Object as PropType<User>,
      required: true,
    },
  },
  setup() {
    const editable = ref(false);
    const editNickname = ref<HTMLFormElement | null>(null);

    // methodsの変わり
    const edit = () => {
      editable.value = true;
      nextTick(() => {
        // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
        (editNickname.value! as HTMLFormElement).focus();
      });
    };

    return {
      editable,
      edit,
      editNickname,
    };
  },
});
/* eslint-disable */
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