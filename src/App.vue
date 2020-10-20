<template>
  <v-app>
    <v-content>
      <v-row class="justify-center">
        <v-col cols="8" class="justify-center">
          <v-layout class="justify-center">
            <v-checkbox
                    id="disable"
                    label="Disable line numbers"
                    v-model="disable"
            /><br>
            <br>Validate:
            <v-radio-group v-model="validateName">
              <v-radio
                      id="none"
                      value="none"
                      label="None"
              />
              <v-radio
                      id="email"
                      value="email"
                      label="Email"
              />
              <v-radio
                      id="telephone"
                      value="telephone"
                      label="Telephone Number"
              />
            </v-radio-group>
            <br><br>
          </v-layout>
        </v-col>
      </v-row>
      <v-row class="justify-center">
        <v-col cols="5">
          <v-lined-textarea
                  :disabled="disable"
                  counter
                  :rows="15"
                  :nowrap="nowrap === 'true'"
                  :validate="validate"
                  :label="label"
                  :hint="hint"
                  v-model="content"
          ></v-lined-textarea>
        </v-col>
      </v-row>
    </v-content>
  </v-app>
</template>

<script>
  import './reset.css';
  import VLinedTextarea from "./VLinedTextarea";

  const sammpleInput = `email@exampleexampleexampleexampleexampleexampleexampleexample.com
firstname.lastname@example.com
email@subdomain.exampexampleexampleexampleexampleexamplele.com
firstname+lastname@example.com
not valid
email@example.co.jp
A long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long long input
(123) 456-7890
(123)456-7890
(123)456-xxxx
123-456-7890
123.456.7890`;

  export default {
    name: 'App',
    components: {
      VLinedTextarea,
    },
    data () {
      return {
        // eslint-disable-next-line
        email: (email) => /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/i.test(email),
        telephone: (telephone) => /^[+]?[(]?[0-9]{3}[)]?[-s.]?[0-9]{3}[-s.]?[0-9]{4,6}$/im.test(telephone),
        content: sammpleInput,
        disable: false,
        height: 300,
        nowrap: 'false',
        resize: 'both',
        validateName: 'none',
        width: 450,
        label: "A demo v-lined-textarea",
        hint: "Write on me please c:"
      }
    },
    computed: {
      validate () {
        switch (this.validateName) {
          case 'email':
            return this.email;
          case 'telephone':
            return this.telephone;
          default:
            return () => true
        }
      }
    }
  }
</script>

<style lang="scss">
  .container {
    margin: 50px auto auto 50px;
  }
</style>