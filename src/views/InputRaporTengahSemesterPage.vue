<template>
  <ion-page>
    <ion-toolbar>
      <ion-buttons slot="start">
        <ion-menu-button color="primary"></ion-menu-button>
      </ion-buttons>
      <ion-grid>
        <ion-row class="ion-justify-content-between ion-align-items-center">
          <ion-col size="6">
            <ion-title class="d-none d-lg-inline-block mt-1" size="small">
              <ion-breadcrumbs :max-items="4" :items-after-collapse="2" class="p-0">
                <ion-breadcrumb style="font-size: 1em" href="/Pages">Pages</ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em" href="/pages/Rapor">E - Rapor</ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em" href="/pages/Rapor/TahunAjaranRapor">Tahun Ajaran
                </ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em" href="/pages/Rapor/TahunAjaranRapor/PesertaDidikRapor">Peserta
                  Didik </ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em"
                  href="/pages/Rapor/TahunAjaranRapor/PesertaDidikRapor/InputNilaiPesertaDidikRapor">Detail</ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em"
                  href="/pages/Rapor/TahunAjaranRapor/PesertaDidikRapor/InputNilaiPesertaDidikRapor/InputRapor">Input</ion-breadcrumb>
              </ion-breadcrumbs>

              <h5 style="margin-left: 11px">Input E - Rapor</h5>
            </ion-title>
          </ion-col>
          <ion-col size-sm="6" size="10">
            <ion-row class="ion-align-items-center ion-justify-content-end goright mt-2" style="margin-right: 20px">
              <div class="btn-group dropstart mb-1 ms-2" style="content: inherit">
                <button class="btn dropdown-toggle text-info text-gradient" type="button" data-bs-toggle="dropdown"
                  aria-expanded="true" style="background-color: transparent">
                  Hi {{ username }}
                </button>
                <ul class="dropdown-menu dropdown-menu-dark">
                  <li><a class="dropdown-item" @click="del()">Logout</a></li>
                </ul>
              </div>
              <div v-if="is_admin == 'true'" class="nav-icon">
                <a href="/SignUp">
                  <ion-icon class="iconButton text-info text-gradient" src="assets/icon/signup.svg"></ion-icon>
                </a>
                <a href="/SignUp" class="d-none d-sm-inline-block mb-1 text-info text-gradient"
                  style="text-decoration: none">&nbsp;Add User</a>
              </div>
              <div>&nbsp;</div>
            </ion-row>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-toolbar>

    <ion-content :fullscreen="true">
      <ion-card>
        <ion-card-content>
          <!-- Aspek Perkembangan dan Pencapaiannya -->
          <ion-card-title class="text-dark mt-3">Aspek Perkembangan dan Pencapaiannya</ion-card-title>
          <ol class="list-group">
            <li class="list-group-item d-flex justify-content-between align-items-start">
              <div class="ms-2 me-auto">
                <ol class="list-group">
                  <li class="list-group-item">
                    Moral dan nilai-nilai Agama<br />
                    <ion-textarea class="custom-textarea" placeholder="Type something here"
                      v-model="formData.text1"></ion-textarea>
                    <ion-note color="danger" v-for="error in v$.text1.$errors" :key="error.$uid">
                      <br />
                      {{ error.$message }}
                    </ion-note>
                  </li>
                  <li class="list-group-item">
                    Motorik Kasar dan Motorik Halus<br />
                    <ion-textarea class="custom-textarea" placeholder="Type something here"
                      v-model="formData.text2"></ion-textarea>
                    <ion-note color="danger" v-for="error in v$.text2.$errors" :key="error.$uid">
                      <br />
                      {{ error.$message }}
                    </ion-note>
                  </li>
                  <li class="list-group-item">
                    Bahasa<br />
                    <ion-textarea class="custom-textarea" placeholder="Type something here"
                      v-model="formData.text3"></ion-textarea>
                    <ion-note color="danger" v-for="error in v$.text3.$errors" :key="error.$uid">
                      <br />
                      {{ error.$message }}
                    </ion-note>
                  </li>
                  <li class="list-group-item">
                    Kognitif<br />
                    <ion-textarea class="custom-textarea" placeholder="Type something here"
                      v-model="formData.text4"></ion-textarea>
                    <ion-note color="danger" v-for="error in v$.text4.$errors" :key="error.$uid">
                      <br />
                      {{ error.$message }}
                    </ion-note>
                  </li>
                  <li class="list-group-item">
                    Sosial-emosional<br />
                    <ion-textarea class="custom-textarea" placeholder="Type something here"
                      v-model="formData.text5"></ion-textarea>
                    <ion-note color="danger" v-for="error in v$.text5.$errors" :key="error.$uid">
                      <br />
                      {{ error.$message }}
                    </ion-note>
                  </li>
                  <li class="list-group-item">
                    Seni<br />
                    <ion-textarea class="custom-textarea" placeholder="Type something here"
                      v-model="formData.text6"></ion-textarea>
                    <ion-note color="danger" v-for="error in v$.text6.$errors" :key="error.$uid">
                      <br />
                      {{ error.$message }}
                    </ion-note>
                  </li>
                </ol>
              </div>
              <!-- <span class="badge bg-primary rounded-pill">14</span> -->
            </li>
          </ol>

          <div>
            <ion-row class="ion-justify-content-center row-button mt-4 mb-3">
              <ion-col size="6" size-sm="2">
                <a class="btn btn-danger"
                  href="/pages/Rapor/TahunAjaranRapor/PesertaDidikRapor/InputNilaiPesertaDidikRapor"
                  role="button">Batalkan</a>
              </ion-col>
              <ion-col size="6" size-sm="2">
                <a class="btn btn-primary" role="button" @click="submitForm()">Simpan</a>
              </ion-col>
            </ion-row>
          </div>
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent, reactive, computed } from "vue";
import { useVuelidate } from "@vuelidate/core";
import { required, integer } from "@vuelidate/validators";
import {
  IonButtons,
  IonContent,
  IonMenuButton,
  IonPage,
  IonTitle,
  IonToolbar,
  IonCol,
  IonGrid,
  IonRow,
  IonCard,
  IonCardContent,
  IonCardTitle,
  IonTextarea,
  // IonSearchbar
} from "@ionic/vue";
import axios from "axios";

export default defineComponent({
  name: "PesertaDidikPage",
  components: {
    IonButtons,
    IonContent,
    IonMenuButton,
    IonPage,
    IonTitle,
    IonToolbar,
    IonCol,
    IonGrid,
    IonRow,
    IonCard,
    IonCardContent,
    IonCardTitle,
    IonTextarea,
    // IonSearchbar
  },
  data() {
    return {
      username: localStorage.getItem("username"),
      is_admin: localStorage.getItem("is_admin"),
    };
  },
  props: ["tahun", "kelas", "id_siswa", "semester"],
  setup() {
    const formData = reactive({
      text1: "",
      text2: "",
      text3: "",
      text4: "",
      text5: "",
      text6: "",
    });

    const rules = computed(() => {
      return {
        text1: {
          required,
        },
        text2: {
          required,
        },
        text3: {
          required,
        },
        text4: {
          required,
        },
        text5: {
          required,
        },
        text6: {
          required,
        },
      };
    });

    const v$ = useVuelidate(rules, formData);

    return { formData, v$ };
  },
  methods: {
    async submitForm() {
      const result = await this.v$.$validate();

      if (!result) {
        console.log(result);
        alert("failed");
      } else {
        const json = JSON.stringify({
          text1: this.formData.text1,
          text2: this.formData.text2,
          text3: this.formData.text3,
          text4: this.formData.text4,
          text5: this.formData.text5,
          text6: this.formData.text6,
          periode: "tengah_semester",
          semester: this.semester,
        });
        console.log(json);
        await axios
          .post("http://31.187.72.73:81/API/rapor/" + this.id_siswa, json, {
            headers: {
              "Access-Control-Allow-Origin": "*",
              "Access-Control-Allow-Credentials": "true",
              "Content-Type": "application/json",
              "Authorization": "Bearer " + localStorage.getItem("access_token"),
            },
            withCredentials: true,
          })
          .then((response) => {
            console.log(response);
            alert("Success");
            window.location.href = "/pages/Rapor/" + this.tahun + "/" + this.kelas + "/" + this.id_siswa;
          })
          .catch((error) => {
            let status = error.response.data.msg;
            if (status == "Missing Authorization Header") {
              alert("Anda belum login");
              window.location.href = "/SignIn";
            }
            else if (status == "Token has expired") {
              alert("Sesi telah berakhir, silahkan login kembali");
              window.location.href = "/SignIn";
            }
          });
      }
    },
    del() {
      let headers = {
        Authorization: "Bearer " + localStorage.getItem("access_token"),
      };

      axios
        .delete("http://31.187.72.73:81/API/auth/logout", { headers })
        .then((response) => {
          console.log(response);
          localStorage.clear();
          alert("Anda berhasil keluar");
        })
        .catch((error) => {
          console.log(error.response.data);
        });
    },
  },
});
</script>

<style scoped>
/* template style */

ion-col {
  padding: 0;
}

/* Textarea style */

ion-textarea.custom-textarea {
  --background: #373737;
  --color: #fff;
  --padding-end: 10px;
  --padding-start: 10px;
  --placeholder-color: #ddd;
  --placeholder-opacity: 0.8;
}

/* Icon navbar style */

a .iconButton {
  color: #67748e;
  text-decoration: none;
  margin-left: 20px;
  font-size: 20px;
}

/* Searchbar Style */

.search-box {
  width: fit-content;
  height: fit-content;
  position: relative;
  color: black;
}

.input-search {
  height: 40px;
  width: 50px;
  border-style: none;
  padding: 10px;
  font-size: 18px;
  letter-spacing: 2px;
  outline: none;
  border-radius: 25px;
  transition: all 0.5s ease-in-out;
  background-color: transparent;
  padding-right: 40px;
  color: black;
}

.input-search::placeholder {
  color: rgba(0, 0, 0, 0.5);
  font-size: 18px;
  letter-spacing: 2px;
  font-weight: 100;
}

.btn-search {
  width: 40px;
  height: 40px;
  border-style: none;
  font-size: 20px;
  font-weight: bold;
  outline: none;
  cursor: pointer;
  border-radius: 50%;
  position: absolute;
  right: 0px;
  color: black;
  background-color: transparent;
  pointer-events: painted;
  top: -1.5px;
}

.btn-search:focus~.input-search {
  width: 230px;
  border-radius: 10px;
  background-color: white;
  border-bottom: 1px solid rgba(255, 255, 255, 0.5);
  transition: all 500ms cubic-bezier(0, 0.11, 0.35, 2);
}

.input-search:focus {
  width: 230px;
  border-radius: 0px;
  background-color: transparent;
  border-bottom: 1px solid rgba(255, 255, 255, 0.5);
  transition: all 500ms cubic-bezier(0, 0.11, 0.35, 2);
}

.text-info {
  color: #17c1e8 !important;
}

.text-gradient {
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  position: relative;
  z-index: 1;
}

.text-gradient.text-info {
  background-image: linear-gradient(310deg, #2152ff, #21d4fd);
}

.text-gradient.text-dark {
  background-image: linear-gradient(310deg, #141727, #3a416f);
}

/* content style */

[data-href] {
  cursor: pointer;
}

.noted {
  font-size: 12px;
}

.noted ul li {
  list-style-type: none;
  list-style: none;
}

/* small laptop dimension */

@media only screen and (max-width: 1280px) {
  .btn-search:focus~.input-search {
    width: 250px;
  }

  .input-search:focus {
    width: 250px;
  }

  th,
  td {
    width: 160px;
  }

  .action-button {
    padding: 5px 12px;
    font-size: 12px;
  }
}

/* tablet dimension */

@media only screen and (max-width: 990px) {
  .btn-search:focus~.input-search {
    width: 200px;
  }

  .input-search:focus {
    width: 200px;
  }

  th,
  td {
    font-size: 12px;
  }
}

/* large phone dimension */

@media only screen and (max-width: 575px) {
  .goright {
    position: relative;
    left: 60px;
  }

  th,
  td {
    width: 150px;
  }

  /* .title-table {
        font-size: 12px;
        margin-top: 10px;
    } */
  .tambah {
    padding: 10px;
    font-size: 10px;
    /* position: relative;
        left: 20px;
        height: 30px; */
  }
}

/* large phone dimension */

@media only screen and (max-width: 426px) {
  .search-box {
    position: absolute;
    right: 34%;
  }

  .btn-search:focus~.input-search {
    width: 200px;
  }

  .input-search:focus {
    width: 200px;
  }
}

/* small phone dimension */

@media only screen and (max-width: 376px) {
  .search-box {
    position: absolute;
    right: 41%;
  }

  .btn-search:focus~.input-search {
    width: 180px;
  }

  .input-search:focus {
    width: 180px;
  }
}

@media only screen and (max-width: 320px) {
  .search-box {
    position: absolute;
    right: 50%;
  }

  .btn-search:focus~.input-search {
    width: 150px;
  }

  .input-search:focus {
    width: 150px;
  }
}
</style>
