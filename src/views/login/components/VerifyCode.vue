<script setup lang="ts" name="VerifyCode">
import { useImageVerify } from "@/hooks";
type Props = {
  code?: string;
  width?: number;
  height?: number;
};
type Emit = {
  (e: "update:code", code: string): string;
};
const props = withDefaults(defineProps<Props>(), {
  code: "",
  width: 140,
  height: 40,
});
const emit = defineEmits<Emit>();
const { domRef, imgCode, setImgCode, getImgCode } = useImageVerify(
  props.width,
  props.height
);
watch(
  () => props.code,
  (val) => {
    if (val) setImgCode(val);
  }
);
watch(imgCode, (val) => {
  emit("update:code", val);
});
defineExpose({ getImgCode });
</script>
<template>
  <canvas
    ref="domRef"
    :width="props.width"
    :height="props.height"
    @click="getImgCode"
  ></canvas>
</template>
<style scoped lang="less"></style>
