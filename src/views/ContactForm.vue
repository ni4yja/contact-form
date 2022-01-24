<template>
  <div class="container">
    <div class="section">
      <div class="card is-horizontal columns">
        <div class="card-image column is-two-fifths p-0">
          <figure class="image">
            <img alt="programming" src="../assets/programming.jpg" />
          </figure>
        </div>
        <div class="card-content column is-three-fifths p-6">
          <p class="title">Contact us</p>
          <form @submit.prevent="onSubmit">
            <div class="columns mt-4">
              <div class="column">
                <fieldset>
                  <legend>Personal Info</legend>
                  <BaseInput 
                    v-model="contact.name" 
                    label="Name" 
                    type="text"
                  />
                  <BaseInput 
                    v-model="email" 
                    :error="emailError"
                    label="Mail"
                    type="email"
                  />
                  <BaseInput 
                    v-model="contact.phone"
                    label="Phone"
                    type="tel"
                  />
                </fieldset>
              </div>
              <div class="column">
                <fieldset>
                  <legend>Message</legend>
                  <BaseTextarea v-model="contact.message" label="Message" />
                </fieldset>
              </div>
            </div>
            <fieldset>
              <legend>Services</legend>
              <BaseRadioGroup
                v-model="contact.services"
                label="Services"
                name="services"
                :options="services"
              />
            </fieldset>
            <button type="submit" class="button is-primary mt-4">Send Message</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import { useField } from 'vee-validate'
export default {
  data() {
    return {
      contact: {
        name: "",
        mail: "",
        phone: "",
        message: "",
        services: 0
      },
      services: [
        { label: 'Web Design', value: 0 },
        { label: 'Web Development', value: 1 },
        { label: 'Graphic Design', value: 2 },
        { label: 'Logo', value: 3 }
      ]
    };
  },
  setup () {
    function onSubmit () {
      alert('Submitted')
    }

    const { value: email, errorMessage: emailError } = useField('email', function (value) {
      if (!value) return 'This field is required'

      const regex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        if (!regex.test(String(value).toLowerCase())) {
          return 'Please enter a valid email address'
        }

      return true
    })

    return {
      onSubmit,
      email: email,
      emailError: emailError
    }
  },
  methods: {
    sendForm () {
      axios.post(
        'https://my-json-server.typicode.com/ni4yja/contact-form/contact',
        this.contact
      )
        .then(function (response) {
          console.log('Response', response)
        })
        .catch(function (err) {
          console.log('Error', err)
        })
    }
  }
};
</script>

<style>
</style>