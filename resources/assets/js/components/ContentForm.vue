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

          <div class="field is-grouped">
            <div class="control">
              <button class="button is-link">Submit</button>
            </div>
            <div class="control">
              <button class="button is-text">Cancel</button>
            </div>
          </div>

        </div>

        <!-- Display the page -->
        <div class="column is-8">

          <section class="hero is-primary">
            <div class="hero-body">
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

              <div class="text-center" v-html="content">

              </div>

              <div class="columns text-center">
                <div class="column">

                  <div class="tile is-parent">

                    <article class="tile is-child notification is-info">
                      <p class="title">Middle tile</p>
                      <figure class="image is-4by3">
                        <img src="https://bulma.io/images/placeholders/640x480.png">
                      </figure>
                      <p>
                        <a class="button is-light">Button</a>
                      </p>
                    </article>

                  </div>

                </div>
                <div class="column">

                  <div class="tile is-parent">

                    <article class="tile is-child notification is-info">
                      <p class="title">Middle tile</p>
                      <figure class="image is-4by3">
                        <img src="https://bulma.io/images/placeholders/640x480.png">
                      </figure>
                      <p>
                        <a class="button is-light">Button</a>
                      </p>
                    </article>

                  </div>

                </div>
                <div class="column">

                  <div class="tile is-parent">

                    <article class="tile is-child notification is-info">
                      <p class="title">Middle tile</p>
                      <figure class="image is-4by3">
                        <img src="https://bulma.io/images/placeholders/640x480.png">
                      </figure>
                      <p>
                        <a class="button is-light">Button</a>
                      </p>
                    </article>

                  </div>

                </div>
              </div>



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
            content:     'The body content'
          };
        },
        components: {
          'editor': Editor // <- Important part
        },
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
