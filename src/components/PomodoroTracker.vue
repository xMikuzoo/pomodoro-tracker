<script lang="ts" setup>
import { Button } from "@/components/ui/button";
import type { SessionTimeKey } from "@/types";
import { SessionTime } from "@/types/enums";
import { CirclePause, CirclePlay, CircleStop } from "lucide-vue-next";
import { computed, onMounted, ref } from "vue";
import ModeSelect from "./ModeSelect.vue";

const DEFAULT_MODE = "focus" as SessionTimeKey;

const sessionMode = ref<SessionTimeKey>(DEFAULT_MODE);
const sessionElapsedTime = ref(0);
const sessionTime = ref(0);

let intervalId: number | undefined = undefined;

const isSessionRunning = computed(() => !!intervalId);

async function runSession() {}

function stopSession() {}

function setMode(mode: SessionTimeKey) {
  sessionTime.value = SessionTime[mode];
  sessionElapsedTime.value = 0;
}

onMounted(() => {
  setMode(DEFAULT_MODE);
});
</script>
<template>
  <div class="flex flex-col items-center justify-center h-full">
    <ModeSelect v-model="sessionMode" @update:model-value="setMode" />
    <div class="p-2"></div>
    <div class="w-fit flex gap-2">
      <Button v-if="!isSessionRunning" @click="runSession()">
        <CirclePlay class="size-5" /> Start</Button
      >
      <Button>
        <CirclePause class="size-5" />
        {{ isSessionRunning ? "Pause" : "Resume" }}</Button
      >
      <Button @click="stopSession()">
        <CircleStop class="size-5" /> Stop</Button
      >
    </div>
  </div>
</template>
