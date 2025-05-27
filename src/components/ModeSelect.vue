<script lang="ts" setup>
import { ToggleGroup, ToggleGroupItem } from "@/components/ui/toggle-group";
</script>
<template>
  <ToggleGroup
    type="single"
    class="[&>*]:px-4"
    @update:model-value="$emit('update:modelValue', $event)"
  >
    <ToggleGroupItem value="focus"> Focus </ToggleGroupItem>
    <ToggleGroupItem value="shortBreak"> Short Break </ToggleGroupItem>
    <ToggleGroupItem value="longBreak"> Long Break </ToggleGroupItem>
  </ToggleGroup>
</template>
