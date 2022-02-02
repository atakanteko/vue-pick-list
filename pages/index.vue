<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="12">

      <v-card>
        <div style="display: flex;justify-content: space-around;">
          <PickListContainer v-model="languages"/>
        </div>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import PickListContainer from "../components/PickListContainer";
import languages from '@/assets/languages.json'
export default {
  name: 'IndexPage',
  components: {PickListContainer},
  data() {
    return {
      languages: []
    }
  },
  mounted() {
    this.languages = [...languages]
  }
}
</script>
