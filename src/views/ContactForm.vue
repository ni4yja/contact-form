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
          <p class="title">Contact us, please</p>
          <div class="columns mt-4">
            <div class="column">
              <BaseInput v-model="contact.name" label="Name" type="text" />
              <BaseInput v-model="contact.mail" label="Mail" type="email" />
              <BaseInput v-model="contact.phone" label="Phone" type="tel" />
            </div>
            <div class="column">
              <BaseTextarea v-model="contact.message" label="Message" />
            </div>
          </div>
          <BaseRadioGroup
            v-model="contact.services"
            label="Services"
            name="services"
            :options="services"
          />
          <button class="button is-primary mt-4">Send Message</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BaseRadioGroup from "../components/BaseRadioGroup.vue";

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
  components: { BaseRadioGroup },
};
</script>

<style>
</style>