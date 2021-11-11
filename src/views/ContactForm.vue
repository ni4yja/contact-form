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
          <div class="columns mt-4">
            <div class="column">
              <BaseInput 
                v-model="contact.name"
                label="Name"
                type="text"
              />
              <BaseInput 
                v-model="contact.mail"
                label="Mail"
                type="email"
              />
            <BaseInput 
                v-model="contact.phone"
                label="Phone"
                type="tel"
              />
            </div>
            <div class="column">
              <BaseTextarea 
                v-model="contact.message"
                label="Message"
              />
            </div>
          </div>
          <div class="field">
            <label class="label">Services</label>
            <div class="control">
              <label class="radio">
                <input type="radio" name="answer" checked>
                Web Design
              </label>
              <label class="radio">
                <input type="radio" name="answer">
                Web Development
              </label>
              <label class="radio">
                <input type="radio" name="answer">
                Graphic Design
              </label>
              <label class="radio">
                <input type="radio" name="answer">
                Logo
              </label>
            </div>
          </div>
          <button class="button is-primary mt-4">Send Message</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      contact: {
        name: '',
        mail: '',
        phone: '',
        message: ''
      }
    }
  }
}
</script>

<style>

</style>