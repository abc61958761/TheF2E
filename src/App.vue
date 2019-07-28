<template>
  <v-app>
    <v-expansion-panel>
      <v-expansion-panel-content
        v-for="(item,i) in 7"
        :key="i"
      >
        <template v-slot:header>
          <div>Item</div>
        </template>
        <v-card>
          <v-card-text>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</v-card-text>
        </v-card>
      </v-expansion-panel-content>
    </v-expansion-panel>
    <v-content>
     <v-container fluid fill-height >
      <v-layout>
        <v-flex v-if="false" xs8 pa-4 style="background:#EAEAEA">
          <v-container fluid fill-height >
            <v-layout align-center justify-center>
              <v-flex style="width:300px;text-align:center">
                <span style="display:inline-block;line-height: 300px;height:300px;width:300px;border-radius:300px;background:#EA5548;font-size:24px;color:#FCFCFC">
                  POMORODO
                </span>
                <div style="font-size:14px;color:#333333;line-height:20px">You don’t have any task now, </div>
                <div style="font-size:14px;color:#333333;line-height:20px">please add task first!</div>
                <div style="font-size:10px;color:#333333">POMORODO</div>
              </v-flex>
            </v-layout>
          </v-container>
        </v-flex>
        <v-flex xs8 pa-4 style="background:#EAEAEA">
          <v-container fluid fill-height >
            <v-layout align-center justify-center>
              <v-flex style="width:300px;text-align:center">
                <div>My First Task</div>
                <v-progress-circular
                :rotate="-90"
                :size="300"
                :width="50"
                :value="showWorkTime"
                color="#EA5548"
                >
                  <span style="font-size:40px;color:#333333;font-weight:bold">{{showWorkMin}}:{{showWorkSecond}}</span>
                </v-progress-circular>
                <div>
                  <v-btn fab icon small color="#F8F8F8" @click="workBtn">
                    <v-icon color="#EA5548">play_arrow</v-icon>
                  </v-btn>
                  <v-btn fab icon small color="#F8F8F8" @click="stopBtn">
                    <v-icon color="#ACACAC">pause</v-icon>
                  </v-btn>
                  <v-btn fab icon small color="#F8F8F8" @click="replayBtn">
                    <v-icon color="#ACACAC">replay</v-icon>
                  </v-btn>
                  </div>
                  <div>TASK COMPELETE</div>
                </v-flex>
              </v-layout>
          </v-container>
        </v-flex>
          <!-- <v-layout style="width:400px">
            <v-text-field
            solo
            label="add a new mission…"
            append-icon="add"
            @click:append="addToDo"
            v-model="newMission"
          ></v-text-field>
          </v-layout>
          <v-layout>

          </v-layout>
          <v-layout style="width: 454px;font-size: 176px;color:#FF4384;font-weight: bold;">
            {{showWorkMin}}:{{showWorkSecond}}
          </v-layout>
          <v-layout row>
            <v-list style="width:400px;background:none" class="pa-0">
              <v-list-tile class="pa-0" v-for="mission in toDoList" style="border-bottom:1px solid #003164">
                <v-list-tile-avatar>
                  <v-icon color="indigo">phone</v-icon>
                </v-list-tile-avatar>
                <v-list-tile-content style="font-weight:bold">
                  {{mission}}
                </v-list-tile-content>
                <v-list-tile-action>
                  <v-btn icon fab>
                    <v-icon>play_circle_filled</v-icon>
                  </v-btn>
                </v-list-tile-action>
              </v-list-tile>
            </v-list>
          </v-layout> -->

          <v-flex style="background:#333333;max-width:80px;width:80px;min-width:80px;text-align:center">
            <v-btn flat icon color="#EA5548" style="width:3px">
              <v-icon>pause_circle_filled</v-icon>
            </v-btn>
            <div @click.stop="drawer = !drawer" style="cursor: pointer;text-align:left;position:fixed;bottom: 40px;margin-left:-25px;padding:12px;height:50px;width:90px;border-radius:25px 5px 5px 25px;background:#FFFFFF">
              <span style="display:inline-block;height:25px;width:25px;border-radius:20px;background:#EA5548;"></span>
              <v-icon>edit</v-icon>
            </div>
          </v-flex>
          <v-flex style="border:1px solid #414141;max-width:2px"></v-flex>
          <v-flex v-if="true" style="width:518px;background:#333333;padding:34px">
            <div style="font-size:20px;color:#FCFCFC;font-weight:bold;line-height:24px">ADD NEW TASK</div>
            <div>
              <div style="color:#ACACAC;font-size:14px;font-weight:bold">TASK TITLE</div>
               <v-text-field
                 solo
                 v-model="newMission"
               ></v-text-field>
            </div>
            <div>
              <div style="color:#ACACAC;font-size:14px;font-weight:bold">ESTIMATED TOMOTO</div>
              <div>
                <span v-for="n in toDoList.length" class="mr-2" style="display:inline-block;height:25px;width:25px;border-radius:20px;background:#EA5548;"></span>
                <span v-for="n in disableTomoto" class="mr-2" style="display:inline-block;height:25px;width:25px;border-radius:20px;background:#ACACAC;"></span>
              </div>
            </div>
            <v-btn :disable="toDoList.length >= 10" @click="addToDo" color="#EA5548" style="color:#FCFCFC;font-weight:bold;font-size:14px" block round>ADD TASK</v-btn>
          </v-flex>
          <v-flex v-if="true" style="width:518px;background:#333333;padding:34px">
            <div style="font-size:20px;color:#FCFCFC;font-weight:bold;line-height:24px">TASK LISTS</div>
            <v-tabs
              color="#606060"
              dark
              slider-color="#EA5548"
            >
              <v-tab
                v-for="(item, i) in taskItems"
                :key="i"
                ripple
              >
                {{item}}
              </v-tab>
              <v-tab-item
                v-for="n in 2"
                :key="n"
              >

                <v-expansion-panel>
      <v-expansion-panel-content
        v-for="(item,i) in toDoList"
        :key="i"
      >
        <v-card>
          {{item}}
          <v-card-text>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</v-card-text>
        </v-card>
      </v-expansion-panel-content>
    </v-expansion-panel>

              </v-tab-item>
            </v-tabs>

          </v-flex>
      </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      workSecond: 0,
      workMin: 1,
      toDoList:[],
      newMission: '',
      countDown: '',
      workTime: 0,
      isStart: false,
      isWork: true,
      drawer: null,
      defaultMin: 1,
      defaultSecond: 0,
      taskItems: ['TO DO', 'DONE']
    }
  },
  computed: {
    showWorkSecond: function () {
      if(this.workSecond < 10) {
        return '0'+ this.workSecond;
      }
      return this.workSecond;
    },
    showWorkMin: function() {
      if(this.workMin < 10) {
        return '0'+ this.workMin;
      }
      return this.workMin;
    },
    showWorkTime: function() {
      return (100/60*this.workTime);
    },
    disableTomoto: function() {
      return 10 - this.toDoList.length;
    }
  },
  methods: {
    addToDo() {
      if(!this.newMission || this.toDoList.length >= 10) return
      this.toDoList.push(this.newMission);
      this.newMission = "";
    },
    stopBtn() {
      clearInterval(this.countDown)
      this.isStart = false;
    },
    replayBtn() {
      clearInterval(this.countDown)
      this.workMin = 1;
      this.workSecond = 0;
      this.workTime = this.workMin * 60 + this.workSecond;
      this.isStart = false;
    },
    workBtn() {
      if(this.isStart) return;
      this.countDown = setInterval(this.timeCountDown, 1000)
      this.isStart = true;
    },
    timeCountDown() {
      if(this.workMin <= 0 && this.workSecond <= 0) {
        clearInterval(this.countDown)
        this.workMin = 1;
        this.workTime = this.workMin * 60 + this.workSecond;
        this.isStart = false;
        return;
      }
      if(this.workSecond == 0) {
        this.workMin--;
        this.workSecond = 60;
      }
      this.workTime--;
      this.workSecond--;
    }
  },
  mounted() {
    //do something after mounting vue instance
    this.workTime = this.workMin * 60 + this.workSecond;
  }
}
</script>
<style>
.showDrawer {
  width:518px;
  max-width:518px;
  min-width:518px;
},
.hideDrawer {
  max-width:0;
  min-width:0;
  width:0px;
}
</style>
