<template>
  <div class="container is-fluid">

    <div class="notification">

      <div class="columns">
        <div class="column is-4">

          <div class="field">
            <label class="label">Heading</label>
            <div class="control">
              <input class="input" v-model="heading" type="text" placeholder="Text input">
            </div>
          </div>

          <div class="field">
            <label class="label">Subtitle</label>
            <div class="control">
              <input class="input" v-model="subtitle" type="text" placeholder="Text input">
            </div>
          </div>

          <div class="field">
            <label class="label">Welcome blurb</label>
            <div class="control">
              <editor v-model="content"></editor>
            </div>
          </div>

          <input type="file" @change="onFileChange" />

          <div id="preview">
            <img v-if="url" :src="url" />
          </div>


        </div>

        <!-- Display the page -->
        <div class="column is-8">

          <section class="hero is-primary">
            <div class="hero-body" :style="{ backgroundImage: 'url(' + url + ')' }">
              <div class="container">
                <h1 class="title">
                  {{ heading }}
                </h1>
                <h2 class="subtitle">
                  {{ subtitle }}
                </h2>
              </div>
            </div>
          </section>

          <section class="hero is-light is-bold">
            <div class="hero-body">

              <div class="text-center" v-html="content"> </div>

            </div>
          </section>

        </div>


      </div>

    </div>
  </div>
</template>


<script>
    // es modules
    import Editor from '@tinymce/tinymce-vue';

    export default {
        data() {
          return {
            heading:  'Heading',
            subtitle: 'Subtitle',
            content:  'The body content',
            url:       null,
          };
        },
        components: {
          'editor': Editor // <- Important part
        },
        methods: {
          onFileChange(e) {
            const file = e.target.files[0];
            this.url = URL.createObjectURL(file);
          }
        },
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
