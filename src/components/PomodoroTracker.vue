<script lang="ts" setup>
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { SessionTime } from "@/types/enums";
import { useCountdown } from "@vueuse/core";
import { CirclePause, CirclePlay, CircleStop } from "lucide-vue-next";
import { computed, onMounted, ref, watch } from "vue";
import ModeSelect from "./ModeSelect.vue";
import SessionTimeDisplay from "./TimeDisplay.vue";

const DEFAULT_MODE = "focus";

const sessionMode = ref<string>(DEFAULT_MODE);
const sessionTime = ref();
const isSessionRunning = ref(false);
const sessionsDone = ref(0);

const { remaining, start, stop, pause, resume } = useCountdown(sessionTime, {
  onComplete() {
    isSessionRunning.value = false;
    if (sessionMode.value === "focus") {
      sessionsDone.value++;
      playNotification();
    }
    if (sessionsDone.value < 4) {
      if (sessionMode.value === "focus") {
        setSessionMode("shortBreak");
      } else {
        setSessionMode("focus");
      }
      return;
    }
    if (sessionMode.value === "longBreak") {
      sessionsDone.value = 0;
      setSessionMode("focus");
      return;
    }
    setSessionMode("longBreak");
  },
  onTick() {},
});

const sessionProgress = computed(() =>
  remaining.value
    ? ((sessionTime.value - remaining.value) / sessionTime.value) * 100
    : 0
);

function setSessionMode(mode: string) {
  stopSession();
  sessionMode.value = mode;
  sessionTime.value = SessionTime[mode];
  remaining.value = sessionTime.value;
}

function playNotification() {
  const audio = new Audio("/public/beer-open-made-with-Voicemod.mp3");
  audio.play();
}

function runSession() {
  start();
  isSessionRunning.value = true;
}

function stopSession() {
  stop();
  isSessionRunning.value = false;
}

function pauseSession() {
  pause();
  isSessionRunning.value = false;
}

function resumeSession() {
  resume();
  isSessionRunning.value = true;
}

watch(sessionMode, (newMode) => {
  setSessionMode(newMode);
});

onMounted(() => {
  setSessionMode(DEFAULT_MODE);
});
</script>
<template>
  <Card>
    <CardContent class="flex flex-col items-center gap-4 min-w-96">
      <ModeSelect v-model="sessionMode" />
      <SessionTimeDisplay
        :remaining-time="remaining"
        :session-progress="sessionProgress"
      />
      <div class="flex text-sm text-muted-foreground flex-col">
        Sessions Done:
        <div class="min-h-6 flex justify-between gap-1 w-full py-2">
          <div
            v-for="i in 4"
            :key="i"
            class="rounded-md flex items-center w-4 h-4"
            :class="i <= sessionsDone ? 'bg-primary' : 'bg-primary-foreground'"
          />
        </div>
      </div>
      <div class="w-full grid grid-cols-3 gap-2 [&>*]:hover:cursor-pointer">
        <Button size="sm" @click="runSession()">
          <CirclePlay class="size-5" /> Start</Button
        >
        <Button
          size="sm"
          @click="isSessionRunning ? pauseSession() : resumeSession()"
        >
          <CirclePause class="size-5" />
          {{ isSessionRunning ? "Pause" : "Resume" }}
        </Button>
        <Button size="sm" @click="stopSession()" :disabled="!isSessionRunning">
          <CircleStop class="size-5" /> Stop</Button
        >
      </div>
    </CardContent>
  </Card>
</template>
