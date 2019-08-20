<template>
    <div>
        <h1>线性进度条---外显</h1>
        <my-progress :show-text=false :percentage=0 />
        <my-progress :percentage=50 />
        <my-progress :percentage=90 status='success'/>
        <my-progress :percentage=30 status='false'/>

        <h1>线性进度条---内显</h1>
        <my-progress  :percentage=0 :text-inside='true' :strokeWidth='18'/>
        <my-progress  :percentage=50 :text-inside='true' :strokeWidth='18'/>
        <my-progress  color='hotpink' :percentage=90 :text-inside='true' status='success' :strokeWidth='18'/>
        <my-progress  :percentage=40 :text-inside='true' status='false' :strokeWidth='18'/>

        <h1>环形进度条---内显</h1>
        <my-progress  :percentage=0 type='circle' />
        <my-progress  :percentage=90 type='circle' />
        <my-progress  :percentage=50 type='circle' status='success'/>
        <my-progress  :percentage=20 type='circle' status='false'/>
    </div>
</template>

<script>
import myProgress from "./Progress";
export default {
  data() {
    return {};
  },
  components: {
    myProgress
  }
};
</script>

<style>
</style>