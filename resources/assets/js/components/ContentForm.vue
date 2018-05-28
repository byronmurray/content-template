<template>

<div class="">
  <div class="columns">

    <div class="column is-4">

      <div class="is-fixed">

        <div class="company-section">


          <span class="title is-size-4">Company details</span>
          <i class="fas fa-sort-up is-pulled-right active" @click="$event.target.classList.toggle('active')"></i>


          <div class="collapse">
            <div class="fileContainer">
              <label class="label">Conpany Logo</label>
              <input type="file" @change="onFileChangeLogo" />
            </div>

            <div v-if="logoUrl" class="field">
              <label class="label">Company Name</label>
              <div class="control">
                <input class="input" v-model="name" type="text">
              </div>
            </div>

            <div v-if="name" class="field">
              <label class="label">Company Phone</label>
              <div class="control">
                <input class="input" v-model="phone" type="text">
              </div>
            </div>

            <div v-if="phone" class="field">
              <label class="label">Company Email</label>
              <div class="control">
                <input class="input" v-model="email" type="text">
              </div>
            </div>
          </div>

        </div>

        <div class="hero-section">
          <span class="title is-size-4">Cover Content</span>
          <i class="fas fa-sort-up is-pulled-right active" @click="$event.target.classList.toggle('active')"></i>

          <div class="collapse">
            <div class="field">
              <label class="label">Cover heading</label>
              <div class="control">
                <input class="input" v-model="heading" type="text" placeholder="Text input">
              </div>
            </div>

            <div v-if="heading" class="field">
              <label class="label">Cover subtitle</label>
              <div class="control">
                <input class="input" v-model="subtitle" type="text" placeholder="Text input">
              </div>
            </div>

            <div v-if="heading" class="fileContainer">
              <label class="label">Cover image</label>
              <input type="file" @change="onFileChangeHero" />
            </div>
          </div>

        </div>

        <div class="body-section">
          <span class="title is-size-4">Body Content details</span>
          <i class="fas fa-sort-up is-pulled-right active" @click="$event.target.classList.toggle('active')"></i>

          <div class="collapse">
            <div class="field">
              <label class="label">Welcome blurb</label>
              <div class="control">
                <editor v-model="content"></editor>
              </div>
            </div>
          </div>

        </div>

        <div class="call-to-action-section">
          <span class="title is-size-4">Call to actions</span>
          <i class="fas fa-sort-up is-pulled-right active" @click="$event.target.classList.toggle('active')"></i>

          <div class="collapse">
            <div v-for="(row, index) in rows">
              <span class="title is-size-6">Card title {{ index +1 }}</span>
              <i class="fas fa-sort-up is-pulled-right" @click="$event.target.classList.toggle('active')"></i>

              <div class="collapse">
                <div class="field">
                  <div class="control">
                    <input class="input" :id="titleId(index)" type="text" v-model="row.title" placeholder="Enter Title for card heading">
                  </div>
                </div>

                <div class="field">
                  <label class="label">Card Message {{ index +1 }}</label>
                  <div class="control">
                    <textarea class="textarea" v-model="row.description" placeholder="Textarea"></textarea>
                  </div>
                </div>

                <div class="fileContainer">
                  <label class="label">Card image {{ index +1 }}</label>
                  <input type="file" @change="onFileChangeCards($event, index)" :id="index">
                </div>
              </div>

            </div>

            <div>
                <button class="button is-primary" @click="addRow">Add card</button>
                <a v-if="rows.length != 0" class="button is-danger" v-on:click="removeElement(index);" style="cursor: pointer">Remove</a>
            </div>
          </div>
          </div>


      </div>

    </div>

    <!-- Display the page -->
    <div class="column is-8">

    <navbar></navbar>


      <section v-if="heading" class="hero is-primary is-fullheight">
        <div class="hero-body " :style="{ backgroundImage: 'url(' + heroUrl + ')' }">
          <div class="container has-text-centered">
            <h1 class="title is-size-1">
              {{ heading }}
            </h1>
            <h2 class="subtitle is-size-3">
              {{ subtitle }}
            </h2>
            <a class="button is-primary is-inverted is-outlined">button 1</a>
            <a class="button is-primary is-inverted is-outlined">button 2</a>
          </div>
        </div>
      </section>

      <section v-if="content" class="hero is-light is-bold">
        <div class="hero-body">
          <div class="text-center body-content" v-html="content">
          </div>
          <div class="columns">
            <div v-for="(row, index) in rows" class="column">

              <div class="card">

                <div class="card-image" :style="{ backgroundImage: 'url(' + row.url + ')' }">
                    <img v-if="row.url" src="images/placeholder.png" :alt="row.title">
                    <img v-else src="images/1280x960.png" alt="Placeholder image">
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

      <footer v-if="name">
        <div class="">
          <span>@ {{ name }} 2018.</span> <span> {{ phone }} </span> <span> {{ email }} </span>
        </div>
      </footer>


    </div>



  </div>


</div>


</template>


<script>
    import Editor from '@tinymce/tinymce-vue';
    import navbar from './NavBar.vue';

    export default {
        data() {
          return {
            logoUrl:     null,
            name: '',
            phone: '',
            email: '',
            heading:  '',
            subtitle: '',
            content:  '',
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
          onFileChangeLogo(event) {
            const file = event.target.files[0];
            this.logoUrl = URL.createObjectURL(file);
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
