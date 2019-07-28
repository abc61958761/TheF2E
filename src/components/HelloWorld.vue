<template>
  <v-container>
      <VueDragResize :isActive="false" :parentLimitation="true" :aspectRatio="false" :isResizable="false" v-on:resizing="resize" v-on:dragging="resize">
          <v-btn>button</v-btn>

      </VueDragResize>
      <VueDragResize :isActive="false" :parentLimitation="true" :aspectRatio="false" :isResizable="false" v-on:resizing="resize" v-on:dragging="resize">
        <v-card>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">Kangaroo Valley Safari</h3>
              <div> card_text </div>
            </div>
          </v-card-title>
        </v-card>
      </VueDragResize>

  </v-container>
</template>

<script>
  import VueDragResize from 'vue-drag-resize'

  export default {
    components: {
        VueDragResize
    },
    data: () => ({
      width: 0,
       height: 0,
       top: 0,
       left: 0,
    }),
    methods: {
        resize(newRect) {
            this.width = newRect.width;
            this.height = newRect.height;
            this.top = newRect.top;
            this.left = newRect.left;
        }
    }
  }
</script>

<style>

</style>
