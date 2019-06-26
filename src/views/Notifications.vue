<template>
  <v-container
    fluid
    grid-list-xl
    fill-height>
    <v-layout
      justify-center
      align-center
    >
      <v-flex xs12>
        <material-card
          color="green">
          <div
            slot="header"
          >
            <div class="title font-weight-light mb-2">Notifications</div>
            <div class="category">
              See Live Updates of Legal Contracts
            </div>
          </div>

          <v-card-text>
            <v-layout
              row
              wrap>
              <v-flex
                md6
                sm12>
                <h2 class="title font-weight-light mb-3">Notifications</h2>

                <material-notification
                  class="mb-3"
                  color="info"
                  dismissible
                  icon="mdi-bell-plus"
                >

                  Demo Notification
                </material-notification>
              </v-flex>

             
            </v-layout>

           

            <v-snackbar
              :color="color"
              :bottom="bottom"
              :top="top"
              :left="left"
              :right="right"
              v-model="snackbar"
              dark
            >
              <v-icon
                color="white"
                class="mr-3"
              >
                mdi-bell-plus
              </v-icon>
              <v-icon
                size="16"
                @click="snackbar = false"
              >
                mdi-close-circle
              </v-icon>
            </v-snackbar>
          </v-card-text>
        </material-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    color: null,
    colors: [
      'purple',
      'info',
      'success',
      'warning',
      'error'
    ],
    top: true,
    bottom: false,
    left: false,
    right: false,
    snackbar: false
  }),

  methods: {
    snack (...args) {
      this.top = false
      this.bottom = false
      this.left = false
      this.right = false

      for (const loc of args) {
        this[loc] = true
      }

      this.color = this.colors[Math.floor(Math.random() * this.colors.length)]

      this.snackbar = true
    }
  }
}
</script>
