<template>
  <v-container>
    <v-card>
      <template v-slot:title>
        <span class="font-weight-black">Método McCabe-Thiele</span>
      </template>
      <v-card-text class="bg-surface-light pt-4">
        <v-row>
          <v-col cols="12" md="6">

            <v-text-field
              v-model="xD"
              :rules="xDRules"
              placeholder="Ej. 0.85"
              required
              type="number"
              @input="saveToLocalStorage('xD', xD)"
            >
              <template v-slot:label>
                Fracción molar del destilado (x<sub>D</sub>)
              </template>
            </v-text-field>

            <v-text-field
              v-model="xF"
              :rules="xFRules"
              placeholder="Ej. 0.5"
              required
              type="number"
              @input="saveToLocalStorage('xF', xF)"
            >
              <template v-slot:label>
                Fracción molar de la alimentación (x<sub>F</sub>)
              </template>
            </v-text-field>

            <v-text-field
              v-model="xB"
              :rules="xBRules"
              placeholder="Ej. 0.1"
              required
              type="number"
              @input="saveToLocalStorage('xB', xB)"
            >
              <template v-slot:label>
                Fracción molar del producto de fondo (x<sub>B</sub>)
              </template>
            </v-text-field>

            <v-text-field
              v-model="alfa"
              :rules="alfaRules"
              placeholder="Ej. 1.5"
              required
              type="number"
              @input="saveToLocalStorage('alfa', alfa)"
            >
              <template v-slot:label>
                Volatilidad relativa (α)
              </template>
            </v-text-field>

            <v-text-field
              v-model="q"
              :rules="qRules"
              placeholder="Ej. 1.2"
              required
              type="number"
              @input="saveToLocalStorage('q', q)"
            >
              <template v-slot:label>
                Estado de la alimentación (q)
                <span v-if="qDescription" :style="{ color: 'blue' }"> - {{ qDescription }}</span>
              </template>
            </v-text-field>

            <v-text-field
              v-model="f"
              :rules="fRules"
              placeholder="Ej. 1.3"
              required
              type="number"
              @input="saveToLocalStorage('f', f)"
            >
              <template v-slot:label>
                Razón de reflujo (f)
              </template>
            </v-text-field>

          </v-col>
          <v-col cols="12" md="6">
            columna 2
            {{f}}
            <McCabeThiele :alfa="3" :xF="0.36" :xD="0.915" :xB="0.05" :q="1.5" :f="1.5" />
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    valid: false,
    xD: parseFloat(localStorage.getItem('xD')) || 0.85,
    xF: parseFloat(localStorage.getItem('xF')) || 0.5,
    xB: parseFloat(localStorage.getItem('xB')) || 0.1,
    alfa: parseFloat(localStorage.getItem('alfa')) || 1.5,
    q: parseFloat(localStorage.getItem('q')) || 1.2,
    f: parseFloat(localStorage.getItem('f')) || 1.3,
  }),
  computed: {
    xDRules() {
      return [
        value => {
          if (value) return true;
          return 'Este valor es obligatorio.';
        },
        value => !isNaN(value) || 'Debe ser un número.',
        value => (parseFloat(value) > 0) || 'La fracción molar debe ser mayor que 0.',
        value => (parseFloat(value) <= 1) || 'La fracción molar debe ser menor que 1.',
        value => (parseFloat(value) > parseFloat(this.xF)) || 'La fracción molar del destilado debe ser mayor a la fracción molar de la alimentación.',
        value => (parseFloat(value) > parseFloat(this.xB)) || 'La fracción molar del destilado debe ser mayor a la fracción molar del fondo.',
      ];
    },
    xFRules() {
      return [
        value => {
          if (value) return true;
          return 'Este valor es obligatorio.';
        },
        value => !isNaN(value) || 'Debe ser un número.',
        value => (parseFloat(value) > 0) || 'La fracción molar debe ser mayor que 0.',
        value => (parseFloat(value) <= 1) || 'La fracción molar debe ser menor que 1.',
        value => (parseFloat(value) < parseFloat(this.xD)) || 'La fracción molar de la alimentación debe ser menor a la fracción molar del destilado.',
        value => (parseFloat(value) > parseFloat(this.xB)) || 'La fracción molar de la alimentación debe ser mayor a la fracción molar del fondo.',
      ];
    },
    xBRules() {
      return [
        value => {
          if (value) return true;
          return 'Este valor es obligatorio.';
        },
        value => !isNaN(value) || 'Debe ser un número.',
        value => (parseFloat(value) > 0) || 'La fracción molar debe ser mayor que 0.',
        value => (parseFloat(value) <= 1) || 'La fracción molar debe ser menor que 1.',
        value => (parseFloat(value) < parseFloat(this.xD)) || 'La fracción molar del fondo debe ser menor a la fracción molar del destilado.',
        value => (parseFloat(value) < parseFloat(this.xF)) || 'La fracción molar del fondo debe ser menor a la fracción molar de la alimentación.',
      ];
    },
    alfaRules() {
      return [
        value => {
          if (value) return true;
          return 'Este valor es obligatorio.';
        },
        value => !isNaN(value) || 'Debe ser un número.',
        value => (parseFloat(value) > 1) || 'La volatilidad relativa debe ser mayor que 1.',
        value => (parseFloat(value) <= 10) || 'La volatilidad relativa debe ser menor o igual a 10.',
      ];
    },
    qRules() {
      return [
        value => {
          if (value) return true;
          return 'Este valor es obligatorio.';
        },
        value => !isNaN(value) || 'Debe ser un número.',
        value => value >= -1 || 'El valor debe ser mayor o igual a -1.',
        value => value <= 2 || 'El valor debe ser menor o igual a 2.'
      ];
    },
    qDescription() {
      const qValue = parseFloat(this.q);
      if (isNaN(qValue)) return null;
      if (qValue === 1) return 'Líq. saturado';
      if (qValue === 0) return 'Vap. saturado';
      if (qValue > 1) return 'Líq. subenfriado';
      if (qValue > 0 && qValue < 1) return 'Mezcla de líq. y vap.';
      if (qValue < 0) return 'Vap. sobrec.';
      return null;
    },
    fRules() {
      return [
        value => {
          if (value) return true;
          return 'Este valor es obligatorio.';
        },
        value => !isNaN(value) || 'Debe ser un número.',
        value => parseFloat(value) >= 1 || 'El factor de reflujo debe ser mayor o igual a 1.',
        value => parseFloat(value) <= 3 || 'El factor de reflujo debe ser menor o igual a 3 para mantener la eficiencia.',
      ];
    },
  },
  methods: {
    saveToLocalStorage(key, value) {
      localStorage.setItem(key, value);
    },
  },
};
</script>
