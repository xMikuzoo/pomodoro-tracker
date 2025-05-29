<script lang="ts" setup>
import { Progress } from "@/components/ui/progress";
import { computed } from "vue";

const props = defineProps({
  remainingTime: {
    type: Number,
    required: false,
  },
  sessionProgress: {
    type: Number,
    required: true,
  },
});

const sessionProgress = computed(() => {
  return props.sessionProgress;
});

const formatTime = (seconds?: number): string => {
  if (!seconds) return "00:00";
  const minutes = Math.floor(seconds / 60);
  const secs = seconds % 60;
  return `${String(minutes).padStart(2, "0")}:${String(secs).padStart(2, "0")}`;
};
</script>
<template>
  <div class="font-bold text-3xl">{{ formatTime(remainingTime) }}</div>
  <Progress v-model="sessionProgress" />
</template>
