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
                <ion-breadcrumb style="font-size: 1em" href="/pages/TenagaKependidikan">Tenaga
                  Kependidikan</ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em"
                  href="/pages/TenagaKependidikan/TambahTenagaKependidikan">Tambah</ion-breadcrumb>
              </ion-breadcrumbs>
              <h5 style="margin-left: 11px">Tambah Tenaga Kependidikan Non-Guru</h5>
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
              <div v-if="is_admin == 'true'" class="d-flex">
                <div class="nav-icon">
                  <a href="/SignUp">
                    <ion-icon class="iconButton text-info text-gradient" src="assets/icon/signup.svg"></ion-icon>
                  </a>
                </div>
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
      <ion-grid>
        <ion-row>
          <ion-col size-xl="12" size="12">
            <ion-card class="m-5 p-3 rounded text-center">
              <ion-card-header>
                <ion-card-title>
                  <h4>Tambah Data Tenaga Kependidikan Non-Guru</h4>
                </ion-card-title>
              </ion-card-header>
              <ion-card-content class="d-grid gap-3">
                <ion-item fill="outline">
                  <ion-label position="floating">Nama</ion-label>
                  <ion-input placeholder="Masukkan Nama" v-model="formData.nama" required></ion-input>
                  <ion-note color="danger" v-for="error in v$.nama.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>
                <ion-item fill="outline">
                  <ion-label position="floating">Jenis Kelamin</ion-label>
                  <ion-input placeholder="Masukkan Jenis Kelamin" v-model="formData.jenis_kelamin" required></ion-input>
                  <ion-note color="danger" v-for="error in v$.jenis_kelamin.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>
                <ion-item fill="outline">
                  <ion-label position="floating">Tempat, Tanggal Lahir</ion-label>
                  <ion-input placeholder="Masukkan Tempat, Tanggal Lahir" v-model="formData.ttl" required></ion-input>
                  <ion-note color="danger" v-for="error in v$.ttl.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>
                <ion-item fill="outline">
                  <ion-label position="floating">Alamat</ion-label>
                  <ion-input placeholder="Masukkan Alamat" v-model="formData.alamat" required></ion-input>
                  <ion-note color="danger" v-for="error in v$.alamat.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>
                <ion-item fill="outline">
                  <ion-label position="floating">No. HP</ion-label>
                  <ion-input placeholder="Masukkan No. HP" v-model="formData.no_hp" required></ion-input>
                  <ion-note color="danger" v-for="error in v$.no_hp.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>
                <ion-item fill="outline">
                  <ion-label position="floating">Email</ion-label>
                  <ion-input placeholder="Masukkan Email" v-model="formData.email" required></ion-input>
                  <ion-note color="danger" v-for="error in v$.email.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>
                <ion-item fill="outline">
                  <ion-label position="floating">Pendidikan Terakhir</ion-label>
                  <ion-input placeholder="Masukkan Pendidikan Terakhir" v-model="formData.pendidikan_terakhir"
                    required></ion-input>
                  <ion-note color="danger" v-for="error in v$.pendidikan_terakhir.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>
                <ion-item fill="outline">
                  <ion-label position="floating">Tahun Ajaran</ion-label>
                  <ion-input placeholder="Masukkan Tahun Ajaran" v-model="formData.tahun_ajaran" required></ion-input>
                  <ion-note color="danger" v-for="error in v$.tahun_ajaran.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>
                <ion-item fill="outline">
                  <ion-label position="floating">Kelas Mengajar</ion-label>
                  <ion-input placeholder="Masukkan Kelas Mengajar" v-model="formData.kelas_mengajar"
                    required></ion-input>
                  <ion-note color="danger" v-for="error in v$.kelas_mengajar.$errors" :key="error.$uid">
                    {{ error.$message }}
                  </ion-note>
                </ion-item>

                <div>
                  <ion-row class="ion-justify-content-center row-button">
                    <ion-col size="6" size-sm="2">
                      <a class="btn btn-danger" href="/pages/TenagaKependidikan" role="button">Batalkan</a>
                    </ion-col>
                    <ion-col size="6" size-sm="2">
                      <a class="btn btn-success" role="button" @click="submitForm()">Tambah</a>
                    </ion-col>
                  </ion-row>
                </div>
              </ion-card-content>
            </ion-card>
          </ion-col>
        </ion-row>
      </ion-grid>
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
  IonCardHeader,
  IonCardTitle,
  IonInput,
  IonItem,
  IonLabel,
} from "@ionic/vue";
import axios from "axios";

export default defineComponent({
  name: "DashboardPage",
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
    IonCardHeader,
    IonCardTitle,
    IonInput,
    IonItem,
    IonLabel,
  },
  setup() {
    const formData = reactive({
      nama: "",
      jenis_kelamin: "",
      ttl: "",
      alamat: "",
      no_hp: "",
      email: "",
      pendidikan_terakhir: "",
      tahun_ajaran: "",
      kelas_mengajar: "",
    });

    const rules = computed(() => {
      return {
        nama: {
          required,
        },
        jenis_kelamin: {
          required,
        },
        ttl: {
          required,
        },
        alamat: {
          required,
        },
        no_hp: {
          required,
          integer,
        },
        email: {
          required,
        },
        pendidikan_terakhir: {
          required,
        },
        tahun_ajaran: {
          required,
        },
        kelas_mengajar: {
          required,
        },
      };
    });

    const v$ = useVuelidate(rules, formData);

    return { formData, v$ };
  },
  data() {
    return {
      username: localStorage.getItem("username"),
      is_admin: localStorage.getItem("is_admin"),
      nama: "",
      jenis_kelamin: "",
      ttl: "",
      alamat: "",
      no_hp: "",
      email: "",
      pendidikan_terakhir: "",
      tahun_ajaran: "",
      kelas_mengajar: "",
    };
  },

  methods: {
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
          window.location.href = "/SignIn";
        })
        .catch((error) => {
          let status = error.response.data.msg;
          if (status == "Missing Authorization Header") {
            alert("Anda belum login");
            window.location.href = "/SignIn";
          } else if (status == "Token has expired") {
            alert("Sesi telah berakhir, silahkan login kembali");
          }
          window.location.href = "/SignIn";
        });
    },
    async submitForm() {
      const result = await this.v$.$validate();

      if (!result) {
        console.log(result);
        alert("failed");
      } else {
        const json = JSON.stringify({
          nama: this.formData.nama,
          jenis_kelamin: this.formData.jenis_kelamin,
          ttl: this.formData.ttl,
          alamat: this.formData.alamat,
          no_hp: this.formData.no_hp,
          email: this.formData.email,
          pendidikan_terakhir: this.formData.pendidikan_terakhir,
          tahun_ajaran: this.formData.tahun_ajaran,
          kelas_mengajar: this.formData.kelas_mengajar,
        });
        console.log(json);
        axios
          .post("http://31.187.72.73:81/API/tendik/nonguru", json, {
            headers: {
              "Access-Control-Allow-Origin": "*",
              "Access-Control-Allow-Credentials": "true",
              "Content-Type": "application/json",
              Authorization: "Bearer " + localStorage.getItem("access_token"),
            },
            withCredentials: true,
          })
          .then((response) => {
            console.log(response);
            alert("Success");
            window.location.href = "/pages/TenagaKependidikan";
          })
          .catch((error) => {
            let status = error.response.data.msg;
            if (status == "Missing Authorization Header") {
              alert("Anda belum login");
              window.location.href = "/SignIn";
            } else if (status == "Token has expired") {
              alert("Sesi telah berakhir, silahkan login kembali");
              window.location.href = "/SignIn";
            }
          });
      }
    },
  },
});
</script>

<style scoped>
/* template style */

ion-col {
  padding: 0;
}

/* Icon navbar style */

a .iconButton {
  color: #67748e;
  text-decoration: none;
  /* margin-left: 20px; */
  margin-right: -13px;
  font-size: 20px;
}

/* Searchbar Style */

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

/* small laptop dimension */

@media only screen and (max-width: 1280px) {
  .btn-search:focus~.input-search {
    width: 250px;
  }

  .input-search:focus {
    width: 250px;
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
}

/* large phone dimension */

@media only screen and (max-width: 575px) {
  .goright {
    position: relative;
    left: 60px;
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

/* content card style */

ion-checkbox {
  --size: 32px;
  --background-checked: #6815ec;
}

ion-checkbox::part(container) {
  border-radius: 6px;
  border: 2px solid #6815ec;
}

ion-searchbar {
  --border-radius: 12px;
  width: 40%;
}

a {
  color: white;
  text-decoration: none;
  margin-left: 20px;
}

ion-icon {
  color: black;
}

ion-card-title,
ion-card-subtitle {
  color: black;
  font-size: 13px;
}

@media only screen and (max-width: 320px) {
  ion-checkbox {
    --size: 15px;
  }

  .checkbox-custom ion-item {
    font-size: 20px !important;
  }
}
</style>
