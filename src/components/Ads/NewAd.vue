<template>
  <v-container>
    <v-layout row>
      <v-flex xs12 sm6 offset-sm3>
        <h1 class="text--secondary mb-3">Create new Ad</h1>

        <v-form v-model="valid" ref="form" validation class="mb-3">

          <v-text-field
            name="title"
            label="Ad title"
            type="text"
            v-model="title"
            required
            :rules="[v => !!v || 'Title is required']"
          ></v-text-field>

          <v-text-field
            name="description"
            label="Ad description"
            type="text"
            v-model="description"
            multi-line
            :rules="[v => !!v || 'Description is required']"
          ></v-text-field>

        </v-form>

        <v-layout row class="mb-3">
          <v-flex sx12>
            <v-btn
              color="warning"
              class="white--text"
            >
              Upload
              <v-icon right dark>cloud_upload</v-icon>
            </v-btn>

          </v-flex>
        </v-layout>

        <v-layout row>
          <v-flex sx12>
            <img src="https://vuetifyjs.com/static/doc-images/carousel/squirrel.jpg" height="100">
          </v-flex>
        </v-layout>
        <v-layout row>
          <v-flex sx12>
            <v-switch
              label="Add to promo"
              color="primary"
              v-model="promo"
            ></v-switch>
          </v-flex>
        </v-layout>

        <v-layout row>
          <v-flex sx12>
            <v-spacer></v-spacer>
            <v-btn
              :loading="loading"
              :disabled="!valid || loading"
              class="success"
              @click="createAd"
            >Create Ad</v-btn>
          </v-flex>
        </v-layout>

      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    data () {
      return {
        title: '',
        description: '',
        promo: false,
        valid: false
      }
    },
    computed: {
      loading () {
        return this.$store.getters.loading
      }
    },
    methods: {
      createAd () {
        if (this.$refs.form.validate()) {
          const ad = {
            title: this.title,
            description: this.description,
            promo: this.promo,
            imageSrc: 'https://i.ebayimg.com/images/g/PbkAAOxyzTJTjU6j/s-l300.jpg'
          }
          this.$store.dispatch('createAd', ad)
            .then(() => {
              this.$router.push('/list')
            })
            .catch(() => {})
        }
      }
    }
  }
</script>
