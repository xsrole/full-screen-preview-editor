<script setup lang="ts" name="WidgetItem">
import {markRaw} from 'vue'
import {useEditorStore} from '@/store'
const editorStore = useEditorStore()
type Props = {
    id:string
};
const props = defineProps<Props>()

const handleWidgetClick = (e:Event)=>{
    editorStore.canvasEditing = false
    editorStore.editWidgetId = props.id
}
const isEdit = computed(()=>{
    return editorStore.editWidgetId === props.id
})
const target = ref(null)
// onClickOutside(target, (event) =>{
//     editorStore.editWidgetId = ''
// })
</script>
<template>
<div ref="target" class="w-full h-full relative" @click.stop="handleWidgetClick" >
    <div v-if="isEdit"
    class="absolute -top-10px -right-10px w-20px h-20px flex items-center justify-center bg-white rounded-full shadow-md z-10 cursor-pointer transition-transform"
    hover="scale-110"
    @click.stop="editorStore.removeWidget(props.id)"
    >
        <i class="i-ri-close-fill inline-block text-lg"></i>
    </div>
    <div v-if="isEdit"
    class="move absolute -top-10px -left-10px w-20px h-20px flex items-center justify-center bg-white rounded-full shadow-md z-10 cursor-move transition-transform"
    hover="scale-110"
    >
        <i class="i-ri-drag-move-2-fill inline-block text-lg"></i>
    </div>
    <slot/>
</div>
</template>
<style scoped lang="less"></style>
