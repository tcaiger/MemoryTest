<template>
  <v-card width="400" class="mx-auto mt-10">
    <v-card-title>
      <h2>Memory Test</h2>
    </v-card-title>
    <v-card-text>
      <v-form
          v-if="!submitted"
          ref="form"
          @submit.prevent="onSubmit"
      >
        <p>Enter the number you want to test your self on. Hit submit and see if you can remember it.</p>
        <v-text-field
            label="Enter any number"
            v-model="question"
            :rules="[v => !!v || 'A number is required']"
            required
        />
        <v-btn
            class="mt-2"
            color="primary"
            type="submit"
            :loading="loading"
            :disabled="loading"
            large
        >
          Submit
        </v-btn>
      </v-form>
      <div v-else>
        <p>Enter your number from memory and see if you are correct!</p>
        <v-text-field
            label="Enter your answer"
            v-model="answer"
            :success="success"
            :error="this.error"
            :success-messages="successMessages"
            :error-messages="errorMessages"
        />
        <v-alert
            v-if="success"
            prominent
            class="mt-4"
            type="success"
        >
          <v-row align="center">
            <v-col class="grow">Well done! You remembered correctly</v-col>
            <v-col class="shrink">
              <v-btn @click="onRestart">Try again</v-btn>
            </v-col>
          </v-row>
        </v-alert>
      </div>
    </v-card-text>
  </v-card>
</template>

<script>
  export default {
    name: "MemoryTest",
    props: {
      msg: String
    },
    data() {
      return {
        question: "",
        answer: "",
        submitted: false,
        loading: false,
      }
    },
    computed: {
      success() {
        return this.answer.length > 0 && this.question === this.answer
      },
      error() {
        return this.answer.length > 0 && !this.success
      },
      successMessages() {
        return this.success ? ['Success'] : []
      },
      errorMessages() {
        return this.error ? ['Keep trying'] : []
      }
    },
    methods: {
      onSubmit() {
        // validate user input
        if (this.$refs.form.validate()) {

          // add loading effect
          this.loading = true
          setTimeout(() => {
            this.submitted = true
            this.loading = false
          }, 500)
        }
      },
      onRestart() {
        // reset state
        this.submitted = false
        this.question = ''
        this.answer = ''
      }
    }
  }
</script>

<style scoped lang="scss"></style>
