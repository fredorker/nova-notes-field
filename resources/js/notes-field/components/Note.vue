<template>
  <div class="w-full bg-white rounded border border-40 px-2 py-2 flex mb-2 mt-2">
    <div class="rounded-full w-12 h-12 mr-3 overflow-hidden text-center">
      <!-- Image -->
      <img class="w-12 h-12" v-if="note.created_by_avatar_url" :src="note.created_by_avatar_url" alt="">
      <div v-else class="w-12 h-12 text-sm font-bold bg-60 text-40" style="line-height: 3rem;">SYS</div>
    </div>

    <div>
      <!-- Title area -->
      <div class="mb-2">
        <span class="font-bold text-lg text-90">{{ note.created_by ? note.created_by.name : 'System' }}</span>
        <span class="text-xs text-80">{{ formattedCreatedAtDate }}{{ note.system ? ' [System]' : '' }}</span>
        <span
          v-if="!note.system && note.can_delete"
          class="text-xs text-error hover:underline cursor-pointer"
          style="color: #e74c3c;"
          @click="$emit('onDeleteRequested', note)"
        >[Delete]</span>
      </div>

      <!-- Content -->
      <p v-html="note.text"></p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['note'],
  computed: {
    formattedCreatedAtDate() {
      return moment(this.note.created_at).format('DD MMM YYYY HH:mm');
    },
  },
};
</script>
