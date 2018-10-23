<template>
    <Page>
        <ActionBar title="Welcome to Masta Recorder!"/>
        <GridLayout columns="*" rows="*">
          <StackLayout>
            <button v-if="!isRecording" class="button" :text="startRecordingLabel" row="0" col="0" @tap="startRecording"/>
            <button v-else class="button" :text="stopRecordingLabel" row="0" col="1" @tap="stopRecording"/>
          </StackLayout>
        </GridLayout>
    </Page>
</template>

<script>
import { TNSRecorder } from 'nativescript-audio';
  export default {
    data() {
      return {
        startRecordingLabel: 'Start Recording',
        stopRecordingLabel: 'Stop Recording',
        recorder: null,
        isRecording: false
      }
    },
    created(){
      this.recorder = new TNSRecorder();
    },
    methods:{
      startRecording: function(){
        if(this.recorder.hasRecordPermission() == false){
          this.recorder.requestRecordPermission().then(()=>{

                console.log("Recording Started...",this.recorder)
                this.recorder.start({
                  filename: 'test'
                });
                this.isRecording = true;




          })
        }
        else{

              console.log("Recording Started..",this.recorder)
              this.recorder.start();
              this.isRecording = true;

        }

      },
      stopRecording: function(){
          console.log("Recording Stopped..",this.recorder)
        this.recorder.stop();
        this.isRecording = false;
      }
    }
  }
</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }

    .button{
      margin-top: 20px;
      margin-bottom: 20px;
      border-radius: 50%;
      background-color: rgba(123,234,16,0.7);
      color: white;
      width: 80%;
      height: 150px;
    }
</style>
