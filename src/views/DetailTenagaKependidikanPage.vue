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
                <ion-breadcrumb style="font-size: 1em;" href="/Pages">Pages</ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em;" href="/pages/TenagaKependidikan">Tenaga
                  Kependidikan</ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em;"
                  href="/pages/TenagaKependidikan/DetailTenagaKependidikan">Detail</ion-breadcrumb>
              </ion-breadcrumbs>
              <h5 style="margin-left: 11px;">Detail Tenaga Kependidikan</h5>
            </ion-title>
          </ion-col>
          <ion-col size-sm="6" size="10">
            <ion-row class="ion-align-items-center ion-justify-content-end goright mt-2" style="margin-right: 20px;">
              <div class="btn-group dropstart mb-1 ms-2" style="content: inherit;">
                <button class="btn dropdown-toggle text-info text-gradient" type="button" data-bs-toggle="dropdown"
                  aria-expanded="true" style="background-color: transparent;">Hi {{ username }} </button>
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
                  style="text-decoration: none;">&nbsp;Add User</a>
              </div>
              <div>&nbsp;</div>
            </ion-row>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-toolbar>

    <ion-content :fullscreen="true">
      <ion-row class="mt-3 mx-2">
        <ion-col>
          <ion-card class="content-card mb-4 border-0">
            <ion-row>
              <ion-col>
                <h3 class="px-3 py-3 title-table">Biodata Guru & Tenaga Kependidikan</h3>
              </ion-col>
            </ion-row>
            <h2 class="text-center mt-1 mb-4">{{ dataTendik.nama }}</h2>
            <ion-row class="mx-auto form-container">
              <ion-col size="4" style="line-height: 2.5;" class="text-dark text-center form1">
                <ul>
                  <li>Jenis Kelamin :</li>
                  <li>Tempat, tanggal lahir :</li>
                  <li>Alamat :</li>
                  <li>No. Telepon :</li>
                  <li>Email :</li>
                  <li>Pendidikan Terakhir :</li>
                  <li>Tahun Ajaran :</li>
                  <li>Kelas Mengajar :</li>
                  <li>Status :</li>
                </ul>
              </ion-col>
              <ion-col size="4" style="line-height: 2.5;" class="text-dark fw-bold text-center form2">
                <ul>
                  <li>{{ dataTendik.jenis_kelamin }}</li>
                  <li>{{ dataTendik.ttl }}</li>
                  <li>{{ dataTendik.alamat }}</li>
                  <li>{{ dataTendik.no_hp }}</li>
                  <li>{{ dataTendik.email }}</li>
                  <li>{{ dataTendik.pendidikan_terakhir }}</li>
                  <li>{{ dataTendik.tahun_ajaran }}</li>
                  <li>{{ dataTendik.kelas_mengajar }}</li>
                  <li>{{ dataTendik.status }}</li>
                </ul>
              </ion-col>
            </ion-row>
            <!-- <ion-card-content class="px-0 pt-0 pb-2">
    
                            </ion-card-content> -->
          </ion-card>
        </ion-col>
      </ion-row>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
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
} from '@ionic/vue';
import axios from "axios";

export default defineComponent({
  name: 'PesertaDidikPage',
  components: {
    IonButtons,
    IonContent,
    // IonHeader,
    IonMenuButton,
    IonPage,
    IonTitle,
    IonToolbar,
    IonCol,
    IonGrid,
    IonRow,
    IonCard,
  },

  data() {
    return {
      username: localStorage.getItem('username'),
      is_admin: localStorage.getItem('is_admin'),
      dataTendik: [],
    };
  },
  props: ["id"],
  mounted: function () {
    let headers = {
      Authorization: "Bearer " + localStorage.getItem("access_token"),
    };

    axios
      .get("http://31.187.72.73:81/API/tendik/" + this.id, { headers })
      .then((response) => {
        this.dataTendik = response.data;
        console.log(response);
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
          }
          else if (status == "Token has expired") {
            alert("Sesi telah berakhir, silahkan login kembali");
          }
          window.location.href = "/SignIn";
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

/* Icon navbar style */

a .iconButton {
  color: #67748E;
  text-decoration: none;
  margin-left: 20px;
  font-size: 20px;
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
  background-image: linear-gradient(310deg, #2152FF, #21D4FD);
}

.text-gradient.text-dark {
  background-image: linear-gradient(310deg, #141727, #3A416F);
}

/* content style */

.form-container ul {
  list-style: none;
  display: inline-block;
  text-align: left;
}

.content-card {
  height: 110%;
}

.form-container {
  justify-content: center;
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
    width: 180px;
  }

  .input-search:focus {
    width: 180px;
  }
}

/* large phone dimension */

@media only screen and (max-width: 575px) {
  .goright {
    position: relative;
    left: 60px
  }

  th,
  td,
  .td-name {
    width: 150px;
  }

  .title-table {
    font-size: 12px;
    margin-top: 10px;
  }
}

/* large phone dimension */

@media only screen and (max-width: 426px) {
  .form {
    font-size: 10px;
  }

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

  .form-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
  }

  .form1 {
    font-size: 10px;
    margin: 0;
    padding: 0;
  }

  .form2 {
    font-size: 10px;
    margin: 0;
    padding: 0;
  }
}
</style>
