<template>
  <div>
    <div class="flex-center position-ref full-height">
      <div class="content">
        <div class="title m-b-md">Kim Potter Dog Training</div>

        <div class="title m-b-md"><small><em>Website Coming Soon</em> <br>Tel: (07941) 392 521 </small></div>

        <div class="links">
            <a href="">Pets and Children</a>
            <a href="">House Training Puppies</a>
            <a href="">Toilet Training Puppies</a>
            <a href="">Aggression Problems</a>
            <a href="">Good Manners</a>
        </div>
        <div class="contact">Contact <a href="caninetrainerkp@gmail.com">caninetrainerkp@gmail.com</a></div>
        
        <!-- contact form -->

        <article v-for="msg in messages"
          :key="msg.text"
          class="message"
          :class="msg.type === 'success' ? 'is-success' : 'is-danger'">
          <div class="message-body">
            {  }
          </div>
        </article>


        <section class="contact-form">
          <div class="field">
            <label class="label">Name</label>
            <div class="control">
              <input v-model="contactName" class="input" type="text">
            </div>
          </div>

          <div class="field">
            <label class="label">Email</label>
            <div class="control">
              <input v-model="contactEmail" class="input" type="email">
            </div>
          </div>

          <div class="field">
            <label class="label">Your Message</label>
            <div class="control">
              <textarea v-model="contactMessage" class="textarea" />
            </div>
          </div>

          <div class="field is-grouped">
            <div class="control">
              <button class="button is-link" @click="sendMessage">
                Send Message
              </button>
            </div>
            <div class="control">
              <button class="button is-text" @click="cancelMessage">
                Cancel
              </button>
            </div>
          </div>
        </section>

      </div>
      </div>
   </div> 
</template>

<script>

export default {
      data () {
        return {
          messages: [],
          contactName: '',
          contactEmail: '',
          contactMessage: ''
        }
      },
      methods: {
        sendMessage () {
          this.messages = []
          this.triggerSendMessageFunction()
        },
        cancelMessage () {},
        resetForm () {
          this.messages = []
          this.contactName = ''
          this.contactEmail = ''
          this.contactMessage = ''
        },
        async triggerSendMessageFunction () {
          try {
            const response = await this.$axios.$post('.netlify/functions/send-contact-email', {
              contactName: this.contactName,
              contactEmail: this.contactEmail,
              message: this.contactMessage
            })
            this.resetForm()
            this.messages.push({ type: 'success', text: response })
          } catch (error) {
            this.messages.push({ type: 'error', text: error.response.data })
          }
        }
      }
    }
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
