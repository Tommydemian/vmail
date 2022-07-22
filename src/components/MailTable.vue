<template>
  <table class="mail-table">
    <tbody>
      <tr
        v-for="email in emails"
        :key="email.id"
        class="clickable"
        :class="{ read: email.read }"
        @click="email.read = true"
      >
        <td>
          <input type="checkbox" />
        </td>
        <td>{{ email.from }}</td>
        <td>
          <p>
            <strong>{{ email.subject }}</strong> -
            {{ email.body }}
          </p>
        </td>
        <td class="date">
          {{ format(new Date(email.sentAt), "MMMM do yyyy") }}
        </td>
        <td><button @click="email.archived = true">Archive</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { format } from "date-fns";

import { Email } from "@/types";

export default defineComponent({
  props: {
    emails: {
      type: Array as PropType<Email[]>,
      required: true,
      default: () => [],
    },
  },
  setup() {
    return {
      format,
    };
  },
});
</script>

<style scoped></style>
