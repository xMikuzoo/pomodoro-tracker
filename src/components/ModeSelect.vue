<script lang="ts" setup>
import { ToggleGroup, ToggleGroupItem } from "@/components/ui/toggle-group";

const sessionMode = defineModel({
  type: String,
  required: true,
});
</script>
<template>
  <ToggleGroup
    type="single"
    class="w-full [&>*]:hover:cursor-pointer"
    v-model="sessionMode"
    variant="outline"
    size="sm"
  >
    <ToggleGroupItem value="focus"> Focus </ToggleGroupItem>
    <ToggleGroupItem value="shortBreak"> Short Break </ToggleGroupItem>
    <ToggleGroupItem value="longBreak"> Long Break </ToggleGroupItem>
  </ToggleGroup>
</template>
