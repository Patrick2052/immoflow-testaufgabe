<script>
import { ref } from 'vue';
import { Button } from 'primevue/button';
import { Dialog } from 'primevue/dialog';
import { InputText } from 'primevue/inputtext';

export default {
    name: 'AddFilePopup',
    components: {
        Button,
        Dialog,
        InputText,
    },
    setup() {
        const visible = ref(false);
        const fileName = ref('');

        const showPopup = () => {
            visible.value = true;
        };

        const hidePopup = () => {
            visible.value = false;
        };

        const addFile = () => {
            console.log('Adding file:', fileName.value);
            hidePopup();
        };

        return {
            visible,
            fileName,
            showPopup,
            hidePopup,
            addFile,
        };
    },
};
</script>

<template>
    <div>
        <Button label="Add File" icon="pi pi-plus" @click="showPopup" />
        <Dialog v-model="visible" title="Add File" :modal="true" :closable="false">
            <InputText v-model="fileName" placeholder="Enter file name" />
            <Button label="Add" icon="pi pi-check" @click="addFile" />
            <Button label="Cancel" icon="pi pi-times" @click="hidePopup" />
        </Dialog>
    </div>
</template>


<style scoped>
/* Add your component-specific styles here */
</style>