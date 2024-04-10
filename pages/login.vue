<template>
  <div class="d-flex align-center justify-center" style="height: 100vh">
    <v-sheet width="500" class="mx-auto">
      <v-card class="rounded" style="padding: 20px">
        <v-row>
          <v-col class="text-center">
            <h5>TO DO APP</h5>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-form ref="form">
              <v-text-field
                v-model="username"
                :rules="[(v) => !!v || 'Username is required']"
                label="Username"
              ></v-text-field>

              <v-text-field
                v-model="password"
                :rules="[(v) => !!v || 'Password is required']"
                label="Password"
              ></v-text-field>

              <v-btn class="mt-2 bg-info" block @click="onSignIn()"
                >Sign In</v-btn
              >
            </v-form>
          </v-col>
        </v-row>
      </v-card>
    </v-sheet>
  </div>
</template>

<script setup>
const router = useRouter();
const username = ref("");
const password = ref("");
const form = ref(null);

const onSignIn = async () => {
  const { valid } = await form.value.validate();
  console.log("ggg", valid);
  if (valid) {
    router.push({ path: "/home" });
  }
};
</script>
