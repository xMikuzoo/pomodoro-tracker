<script setup lang="ts">
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";
import PomodoroTracker from "@/components/PomodoroTracker.vue";
</script>

<template>
  <div
    class="flex items-center justify-center min-h-screen bg-primary-foreground"
  >
    <Card>
      <CardHeader>
        <CardTitle class="text-primary/80 font-bold text-xl"
          >Pomodoro Tracker</CardTitle
        >
        <CardDescription class="text-primary/75">
          A simple Pomodoro timer to help you manage your time effectively.
        </CardDescription>
      </CardHeader>
      <CardContent> <PomodoroTracker /> </CardContent>
    </Card>
  </div>
</template>
