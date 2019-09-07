<template>
  <v-row justify="left ml-4">
    <v-dialog v-model="dialog1" persistent max-width="400px">
      <template v-slot:activator="{ on }">
        <v-btn color="primary text-capitalize subtitle-1" dark v-on="on">Login <i class="text-right fas fa-sign-in-alt"></i></v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">Login</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field v-model="email" :rules="emailRules" label="Email*" v-validate="'required|email'"></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="password" :rules="passwordRules" label="Password*" type="password" required></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <v-flex>
            <small class="subtitle-2 primary--text text-right">Sign Up</small>
          </v-flex>
        </v-card-text>
        <v-card-actions>
          <div class="flex-grow-1"></div>
          <v-btn color="blue darken-1" text @click="dialog1 = false">Cancel</v-btn>
          <v-btn color="blue darken-1" text @click="dialog1 = false">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>


    <v-dialog v-model="dialog2" persistent max-width="400px">
      <template v-slot:activator="{ on }">
        <v-btn color="primary text-capitalize subtitle-1" dark v-on="on">Sign Up<i class="text-right fas fa-sign-in-alt"></i></v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">Sign Up</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field v-model="email" :rules="emailRules" label="Email*" v-validate="'required|email'"></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="password" :rules="passwordRules" label="Password*" type="password" required></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <v-flex>
            <small class="subtitle-2 primary--text text-right">Sign Up</small>
          </v-flex>
        </v-card-text>
        <v-card-actions>
          <div class="flex-grow-1"></div>
          <v-btn color="blue darken-1" text @click="dialog2 = false">Cancel</v-btn>
          <v-btn color="blue darken-1" text @click="dialog2 = false">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
  export default {
    data: () => ({
      dialog1: false,
      dialog2: false,
      valid: false,
      email: '',
      password: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid'
      ],
      passwordRules: [
        v => v.length >= 6 || 'Minimum length is 6 characters'
        // v => /.+@.+/.test(v) || 'E-mail must be valid',
      ],
    }),
  }
</script>