<template>
  <v-layout justify-center>
    <v-flex ref="flex" xs10 sm8 md4>
      <v-container>
        <v-row>
          <v-col cols="12">
            <h1 class="page-title">Gerenciar meus cursos</h1>
          </v-col>
        </v-row>
        <v-form ref="form" lazy-validation>
          <v-row>
            <v-col cols="12">
              <h1>Curso</h1>
              <v-text-field
                color="#60c"
                label="Título"
                :rules="titleRules"
                required
              />
              <v-textarea
                color="#60c"
                label="Descrição"
                :rules="descriptionRules"
                required
              />
            </v-col>
          </v-row>
          <v-row>
            <v-col cols="12">
              <h1>Aulas</h1>
              <resources-list
                name="Aulas"
                :resources="course.classes"
                path="classes/"
              />
            </v-col>
          </v-row>
          <v-btn color="#60c" dark block depressed large @click="submit">
            Salvar
          </v-btn>
        </v-form>
      </v-container>
    </v-flex>
  </v-layout>
</template>

<script scoped>
import courses from '../../../services/http/courses'

export default {
  data() {
    return {
      title: 'Adicionar novo curso',

      titleRules: [v => !!v || 'Digite o título do curso'],
      descriptionRules: [v => !!v || 'Digite uma descrição para o curso'],
    }
  },

  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        const postObject = Object.assign({}, this.form)
        courses.post(postObject).then(res => {})
      }
    },
  },

  head() {
    return {
      title: this.title,
    }
  },
}
</script>

<style scoped>
h1 {
  font-weight: 900;
  font-size: 20px;
  line-height: 24px;
  text-transform: uppercase;

  color: #6600cc;
}
</style>
