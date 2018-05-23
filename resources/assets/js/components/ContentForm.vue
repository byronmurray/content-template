<template>

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

    <input type="file" @change="onFileChangeHero" />

    <div id="preview">
      <img v-if="heroUrl" :src="heroUrl" />
    </div>


    <div v-for="(row, index) in rows">

      <div class="field">
        <label class="label">Title</label>
        <div class="control">
          <input class="input" :id="titleId(index)" type="text" v-model="row.title" placeholder="Enter Title for card heading">
        </div>
      </div>

      <div class="field">
        <label class="label">Message</label>
        <div class="control">
          <textarea class="textarea" v-model="row.description" placeholder="Textarea"></textarea>
        </div>
      </div>

      <label class="fileContainer">
        <input type="file"  @change="onFileChangeCards($event, index)" :id="index">
      </label>

    </div>

    <div>
        <button class="button btn-primary" @click="addRow">Add row</button>
        <a v-if="rows.length != 0" class="button btn-primary" v-on:click="removeElement(index);" style="cursor: pointer">Remove</a>
    </div>
  </div>

  <!-- Display the page -->
  <div class="column is-8">
    <section class="hero is-primary">
      <div class="hero-body" :style="{ backgroundImage: 'url(' + heroUrl + ')' }">
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
        <div class="columns">
          <div v-for="(row, index) in rows" class="column">

            <div class="card">

              <div class="card-image">
                  <img v-if="row.url" :src="row.url" :alt="row.title">
                  <img v-else src="https://bulma.io/images/placeholders/1280x960.png" alt="Placeholder image">
              </div>

              <div class="card-content">

                <div class="title is-4">{{ row.title }}</div>

                <div class="content">
                  {{ row.description }}
                </div>

              </div>
            </div>

          </div>
        </div>

      </div>
    </section>
</div>

</div>




</template>


<script>
    import Editor from '@tinymce/tinymce-vue';


    export default {
        data() {
          return {
            heading:  'Heading',
            subtitle: 'Subtitle',
            content:  'The body content',
            heroUrl:  null,
            rows: [],
            index: false,
          };
        },
        components: {
          'editor': Editor // <- Tinymce Editor
        },
        methods: {

          addRow: function() {
              this.rows.push({
                  title: "",
                  description: "",
                  url: "",
              });
          },

          onFileChangeCards: function(event, index) {
            const file = event.target.files[0];
            Vue.set(this.rows[index], 'url', URL.createObjectURL(file));
          },
          onFileChangeHero(event) {
            const file = event.target.files[0];
            this.heroUrl = URL.createObjectURL(file);
          },

          titleId: function (index) {
            return "tile-" + (index + 1)
          },

          removeElement: function(index) {
              this.rows.splice(index, 1);
          }
      }

    }
</script>
