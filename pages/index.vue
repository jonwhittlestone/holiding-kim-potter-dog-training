<template>
  <div>
    <div class="flex-center mt-24 position-ref full-height">
      <div class="content">
        <div class="title m-b-md">Kim Potter Dog Training</div>

        <div class="pb-24 text-4xl"><small><em>Website Coming Soon</em> <br>Tel: (07941) 392 521 </small></div>

        <div class="links pb-12">
            <a href="">Pets and Children</a>
            <a href="">House Training Puppies</a>
            <a href="">Toilet Training Puppies</a>
            <a href="">Aggression Problems</a>
            <a href="">Good Manners</a>
        </div>
        <div class="pb-12">
          <a href="caninetrainerkp@gmail.com">caninetrainerkp@gmail.com</a>
        </div>
        
        <!-- contact form -->
        <article v-for="msg in messages"
          :key="msg.text"
          class="message"
          :class="msg.type === 'success' ? 'is-success' : 'is-danger'">
          <div class="message-body">
            {{msg.text}}
          </div>
        </article>


        <section class="contact-form w-1/2 mx-auto text-left p-6">
          <div class="row flex">
            <div class="field col w-1/2 pr-4">
              <label class="label">Name</label>
              <div class="control">
                <input v-model="contactName" class="input w-full border border-gray-700" type="text">
              </div>
            </div>

            <div class="field col w-1/2">
              <label class="label">Email</label>
              <div class="control">
                <input v-model="contactEmail" class="input w-full border border-gray-700" type="email">
              </div>
            </div> <!-- /.field -->

          </div>
          <div class="row pt-4">
            <div class="field col">
              <label class="label">Your Message</label>
              <div class="control">
                <textarea v-model="contactMessage" class="textarea border w-full border-gray-700" />
              </div>
            </div>
          </div>

          <div class="field is-grouped py-4">
            <div class="control text-center">
              <button class="button is-link border-gray-700 border px-4" @click="sendMessage">
                Send Message
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
            const response = await this.$axios.$post('/.netlify/functions/send-contact-email', {
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
article.message {
  @apply border mx-8
}

article.message.is-error {
  @apply bg-red-200 border border-red-400 text-red-700 px-4 py-3 rounded relative
}

article.message.is-success {
  @apply bg-green-200 border border-green-400 text-green-700 px-4 py-3 rounded relative
}
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
