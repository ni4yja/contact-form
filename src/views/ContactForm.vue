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
          <form
            :class="{'all-errors' : allErrors }"
            @submit="submit">
            <div class="columns mt-4">
              <div class="column">
                <fieldset>
                  <legend>Personal Info</legend>
                  <BaseInput 
                    :class="{'is-danger': errors.userName}"
                    v-model="userName" 
                    :error="errors.userName"
                    label="Name" 
                    type="text"
                  />
                  <BaseInput
                    :class="{'is-danger': errors.email}"
                    v-model="email" 
                    :error="errors.email"
                    label="Mail"
                    type="email"
                  />
                  <BaseInput
                    :class="{'is-danger': errors.phone}"
                    v-model="phone" 
                    :error="errors.phone"
                    label="Phone"
                    type="tel"
                  />
                </fieldset>
              </div>
              <div class="column">
                <fieldset>
                  <legend>Message</legend>
                  <BaseTextarea
                    v-model="message" 
                    :error="errors.message"
                    label="Message"
                  />
                </fieldset>
              </div>
            </div>
            <fieldset>
              <legend>Services</legend>
              <BaseRadioGroup
                v-model="services"
                :error="services.error"
                label="Services"
                name="services"
                :options="servicesOptions"
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
import { useForm, useField } from 'vee-validate'
export default {
  data() {
    return {
      servicesOptions: [
        { label: 'Web Design', value: 0 },
        { label: 'Web Development', value: 1 },
        { label: 'Graphic Design', value: 2 },
        { label: 'Logo', value: 3 }
      ]
    };
  },
  computed: {
    allErrors() {
      return this.errors.userName
        && this.errors.email
        && this.errors.phone
        && this.errors.message;
    },
  },
  setup () {
    const required = value => {
      const requiredMessage = 'This field is required'
      if (value === undefined || value === null) return requiredMessage
      if (!String(value).length) return requiredMessage

      return true
    }

    const emailCheck = value => {
      const requiredMessage = 'Please enter a valid email address'
      const regex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      if (!regex.test(String(value).toLowerCase())) {
        return requiredMessage
      }

      return true
    }

    const phoneCheck = value => {
      const requiredMessage = 'Please enter a valid phone number'
      const regex = /^\(?(\d{3})\)?[- ]?(\d{3})[- ]?(\d{4})$/
      if (!regex.test(String(value).toLowerCase())) {
        return requiredMessage
      }

      return true
    }

    const minLength = (number, value) => {
      if (String(value).length < number) return 'Please type at least ' + number + ' characters'

      return true
    }

    const maxLength = (number, value) => {
      if (String(value).length > number) return 'Please try to fit into ' + number + ' characters'

      return true
    }

    const anything = () => {
      return true
    }

    const validationSchema = {
      userName: (value) => {
        const req = required(value)
        if (req !== true) return req

        const min = minLength(2, value)
        if (min !== true) return min

        return true
      },

      email: (value) => {
        const req = required(value)
        if (req !== true) return req

        const validEmail = emailCheck(value)
        if (validEmail !== true) return validEmail

        return true
      },

      phone: (value) => {
        const validPhone = phoneCheck(value)
        if (validPhone !== true) return validPhone
        
        return true
      },
      
      message: (value) => {
        const min = minLength(100, value)
        if (min !== true) return min

        const max = maxLength(500, value)
        if (max !== true) return max

        return true
      },

      services: anything
    }

    const { handleSubmit, errors } = useForm({
      validationSchema,
      initialValues: {
        services: 0
      }
    })

    const { value: userName } = useField('userName')
    const { value: email } = useField('email')
    const { value: phone } = useField('phone')
    const { value: message } = useField('message')
    const { value: services } = useField('services')

    const submit = handleSubmit((values, actions) => { 
      axios.post(
        'https://my-json-server.typicode.com/ni4yja/contact-form/contact',
        values
      )
        .then(function (response) {
          console.log('Response', response)
          actions.resetForm()
        })
        .catch(function (err) {
          console.log('Error', err)
        })
    })

    return {
      submit,
      userName,
      email,
      phone,
      message,
      services,
      errors
    }
  },
};
</script>

<style>
</style>