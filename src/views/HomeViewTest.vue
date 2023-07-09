<template>
    <div class="container">
        <a-col span="10">
            <a-form
                :model="formState"
                name="basic"
                :label-col="{ span: 8 }"
                :wrapper-col="{ span: 16 }"
                @finish="onFinish"
                @finishFailed="onFinishFailed"
            >
                <a-form-item
                    label="Name"
                    name="username"
                >
                    <a-input v-model:value="formState.username" />
                </a-form-item>

                <a-form-item
                    label="Code"
                    name="code"
                >
                    <a-input v-model:value="formState.code" />
                </a-form-item>


                <a-form-item :wrapper-col="{ offset: 8, span: 16 }">
                    <a-button type="primary" html-type="submit">Submit</a-button>
                </a-form-item>
            </a-form>
        </a-col>
    </div>
</template>
<script setup lang="ts">
import { reactive } from 'vue';

interface FormState {
    username: string;
    code: string;
}
const formState = reactive<FormState>({
    username: '',
    code: '',
});
const serverUrl ='ws://localhost:5000';
const socket = new WebSocket(serverUrl);
const onFinish = (values: any) => {
    console.log(values)
    socket.send(JSON.stringify(values))
};

const onFinishFailed = (errorInfo: any) => {
    console.log('Failed:', errorInfo);
};

</script>
<style scoped>
.container {
    margin: 40px auto 0 auto;
}
</style>

