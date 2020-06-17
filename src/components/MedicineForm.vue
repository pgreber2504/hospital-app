<template>
  <div class="wrapper">
    <div class="medicine-details">
      <h3>Wprowadź niezbędne dane</h3>

      <form>
        <p>
          <label for>Rodzaj leku</label>
          <select v-model="order.medicine">
            <option
              v-for="(item, index) in tablets"
              :key="index"
              :value="item"
            >{{item.name}}, {{item.quantity}}</option>
          </select>
        </p>

        <p>
          <label for="time">Czas przyjęcia leku</label>
          <select v-model="order.time">
            <option value="8:00">8:00</option>
            <option value="15:00">15:00</option>
            <option value="22:00">22:00</option>
          </select>
        </p>

        <p>
          <label>Data podania leku</label>
          <datepicker class="datepicker" :language="pl" v-model="order.date"></datepicker>
        </p>

        <p>
          <label for>Ilość leku</label>
          <select name id v-model="order.amount">
            <option v-for="n in 10" :key="n" :value="n">{{n}} tab.</option>
          </select>
        </p>

        <p class="fulfill">
          <label>Oddział przesłania leku</label>
          <select v-model="order.hospital">
            <option
              v-for="(item, index) in hospitals"
              :key="index"
              :value="item"
            >{{item.name}}, {{item.address}}</option>
          </select>
        </p>
      </form>
    </div>

    <div class="patient-details">
      <h3>Dane osobowe</h3>

      <form @submit.prevent>
        <p>
          <label for>Imię pacjenta</label>
          <input type="text" @keyup.enter="submitPatient" v-model="order.patientInfo.name" />
        </p>

        <p>
          <label for>Nazwisko pacjenta</label>
          <input type="text" @keyup.enter="submitPatient" v-model="order.patientInfo.surname" />
        </p>

        <p class="fulfill">
          <label for>Nr. PESEL</label>
          <input type="text" @keyup.enter="submitPatient" v-model="order.patientInfo.pesel" />
        </p>

        <p class="fulfill">
          <input class="button" @click="submitPatient" @submit.prevent type="submit" />
        </p>
      </form>
    </div>

    <div v-if="loading" class="lds-heart">
      <div></div>
    </div>

    <div v-if="success" class="success">
      <h4>Twoje zamówienie zostało przyjęte</h4>
    </div>

    <div v-if="errors.length" class="error">
      <h4 v-for="(item, index) in errors" :key="index">* {{item}}</h4>
    </div>
  </div>
</template>

<script>
import datepicker from "vuejs-datepicker";
import { pl } from "vuejs-datepicker/dist/locale";
import { mapState } from "vuex";

export default {
  components: {
    datepicker
  },

  computed: {
    ...mapState(["hospitals", "tablets"])
  },

  data() {
    return {
      order: {
        medicine: null,
        amount: null,
        time: null,
        hospital: null,
        patientInfo: {
          name: "",
          surname: "",
          pesel: ""
        }
      },

      errors: [],
      loading: false,
      success: false,

      date: null,
      pl: pl
    };
  },

  methods: {
    checkForm() {
      this.errors = [];

      if (
        !this.order.medicine ||
        !this.order.amount ||
        !this.order.time ||
        !this.order.hospital ||
        !this.order.patientInfo.name ||
        !this.order.patientInfo.surname ||
        !this.order.patientInfo.pesel
      ) {
        this.errors.push("Musisz uzupełnic wszystkie pola!");
      }

      if (
        /\d/.test(this.order.patientInfo.name) ||
        /\d/.test(this.order.patientInfo.surname)
      ) {
        this.errors.push("Imię i Nazwisko nie mogą zawierac cyfr!");
      }

      if (/[a-zA-Z]+/g.test(this.order.patientInfo.pesel)) {
        this.errors.push("Pesel nie moze zawierac liter!");
      }

      if (!this.errors.length) {
        return true;
      }
    },

    submitPatient() {
      if (this.checkForm()) {
        this.loading = true;

        fetch("https://reqres.in/api/users", {
          method: "POST",
          body: JSON.stringify(this.order),
          headers: {
            "Content-type": "application/json; charset=UTF-8"
          }
        })
          .then(response => response.json())
          .then(json => {
            this.loading = false;
            this.success = true;
            this.order = {
              medicine: null,
              amount: null,
              time: null,
              hospital: null,
              patientInfo: {
                name: "",
                surname: "",
                pesel: ""
              }
            };
            console.log(json);
            setTimeout(() => {
              this.success = false;
            }, 3000);
          })
          .catch(err => {
            console.log(err);
          });
      }
    }
  }
};
</script>

<style lang="scss">
.wrapper {
  box-shadow: 0 0 20px 0 rgba(72, 94, 116, 0.7);
  margin: 80px 10px;
}

.wrapper > * {
  padding: 1em;
}

.medicine-details {
  background-color: #7396b8;
  color: white;
}

.patient-details {
  background-color: #f9feff;
}

.medicine-details form,
.patient-details form {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
  font-size: 0.7rem;
}

.medicine-details form label,
.patient-details form label {
  display: block;
}

.medicine-details form p,
.patient-details form p {
  margin: 0;
}

.patient-details .fulfill,
.medicine-details .fulfill {
  grid-column: 1/3;
}

.medicine-details form select,
.medicine-details form input,
.patient-details form button,
.patient-details form input {
  width: 100%;
  padding: 1em;
  border: 1px solid #c9e6ff;
  font-size: 0.8em;
}

.patient-details form .button {
  background: #c9e6ff;
  border: 0;
  text-transform: uppercase;
}

.patient-details form .button:hover,
.patient-details form .button:focus {
  background-color: #92bde7;
  color: white;
  outline: 0;
  transition: background-color 0.7s ease-out;
}

.datepicker {
  color: black;
}

.error {
  color: red;
  grid-column: 1/3;
  text-align: center;
  font-size: 0.8rem;
}

.success {
  color: rgb(65, 148, 65);
  grid-column: 1/3;
  text-align: center;
}

.lds-heart {
  display: inline-block;
  position: relative;
  left: 80%;
  width: 100px;
  height: 80px;
  margin: 10px;
  transform: rotate(45deg);
  transform-origin: 40px 40px;
}
.lds-heart div {
  top: 32px;
  left: 32px;
  position: absolute;
  width: 32px;
  height: 32px;
  background: #cef;
  animation: lds-heart 1.2s infinite cubic-bezier(0.215, 0.61, 0.355, 1);
}
.lds-heart div:after,
.lds-heart div:before {
  content: " ";
  position: absolute;
  display: block;
  width: 32px;
  height: 32px;
  background: #cef;
}
.lds-heart div:before {
  left: -24px;
  border-radius: 50% 0 0 50%;
}
.lds-heart div:after {
  top: -24px;
  border-radius: 50% 50% 0 0;
}
@keyframes lds-heart {
  0% {
    transform: scale(0.95);
  }
  5% {
    transform: scale(1.1);
  }
  39% {
    transform: scale(0.85);
  }
  45% {
    transform: scale(1);
  }
  60% {
    transform: scale(0.95);
  }
  100% {
    transform: scale(0.9);
  }
}

@media (min-width: 700px) {
  .wrapper {
    display: grid;
    grid-template-columns: 3fr 2fr;
    margin-top: 30vh;
  }

  .wrapper > * {
    padding: 2em;
  }

  .error {
    font-size: inherit;
  }
}

@media (max-width: 321px) {
  .medicine-details form,
  .patient-details form {
    font-size: 0.5em;
  }
}
</style>