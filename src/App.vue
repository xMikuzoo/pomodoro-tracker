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
  <Card class="m-2">
    <CardHeader>
      <CardTitle>Pomodoro Tracker</CardTitle>
      <CardDescription>
        A simple Pomodoro timer to help you manage your time effectively.
      </CardDescription>
    </CardHeader>
    <CardContent><PomodoroTracker /></CardContent>
  </Card>
</template>
