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
                <ion-breadcrumb style="font-size: 1em" href="/pages/Rapor/TahunAjaranRapor">Tahun
                  Ajaran</ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em" href="/pages/Rapor/TahunAjaranRapor/PesertaDidikRapor">Peserta
                  Didik</ion-breadcrumb>
                <ion-breadcrumb style="font-size: 1em"
                  href="/pages/Rapor/TahunAjaranRapor/PesertaDidikRapor/InputNilaiPesertaDidikRapor">Detail</ion-breadcrumb>
              </ion-breadcrumbs>
              <h5 style="margin-left: 11px">Input Nilai E - Rapor</h5>
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
                <div>&nbsp;</div>
              </div>
            </ion-row>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-toolbar>

    <ion-content :fullscreen="true">
      <ion-card class="rounded card-content mt-3 mx-3">
        <ion-card-header class="ion-text-justify">
          <ion-row class="ion-justify-content-between mb-4">
            <ion-col size-xl="4" size-md="4" size-xs="12">
              <h6 class="text-dark">Nama Peserta Didik</h6>
              <h4 v-if="results.length != 0" class="text-dark">{{ results.nama_peserta_didik.nama }}</h4>
            </ion-col>
            <ion-col size-xl="2" size-md="2" size-xs="12">
              <h6 class="text-dark">Rombel</h6>
              <h4 v-if="results.length != 0" class="text-dark">{{ results.nama_peserta_didik.tahun_ajaran }}</h4>
            </ion-col>
            <ion-col size-xl="1" size-md="1" size-xs="12">
              <h6 class="text-dark">Kelas</h6>
              <h4 v-if="results.length != 0" class="text-dark">{{ results.nama_peserta_didik.tingkat_kelas }}</h4>
            </ion-col>
            <!-- <ion-col size-xl="2" size-md="2" size-xs="12">
              <h6 class="text-dark">Kelompok Usia</h6>
              <h4 class="text-dark">6</h4>
            </ion-col> -->
            <ion-col size-xl="3" size-md="3" size-xs="12">
              <h6 class="text-dark">Nomor Induk</h6>
              <h4 v-if="results.length != 0" class="text-dark">{{ results.nama_peserta_didik.nomor_induk }}</h4>
            </ion-col>
          </ion-row>
        </ion-card-header>

        <ion-card-content>
          <!-- <ion-searchbar show-cancel-button="focus" placeholder="Show on Focus"></ion-searchbar> -->
          <div class="table-responsive">
            <table class="table table-borderless table-hover display" id="table-rapor">
              <thead>
                <tr>
                  <th scope="col" class="text-center text-secondary opacity-7">No</th>
                  <th scope="col" class="text-center text-secondary opacity-7">Keterangan</th>
                  <th scope="col" class="text-center text-secondary opacity-7">Aksi</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td class="text-center">1</td>
                  <td class="text-center">Tengah Semester 1</td>
                  <td class="text-center">
                    <div v-if="ishere('tengah_semester', 1) == true">
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/tengah_semester/1/detail/'">
                        <div class="kotak kotak-pink">
                          <ion-icon src="assets/icon/view-icon.svg" class="text-center m-auto"></ion-icon>
                        </div>
                      </a>
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/tengah_semester/1/edit'">
                        <div class="kotak kotak-kuning">
                          <ion-icon src=""></ion-icon>
                        </div>
                      </a>
                      <a @click="delRapot('tengah_semester', 1)">
                        <div class="kotak kotak-merah">
                          <ion-icon src=""></ion-icon>
                        </div>
                      </a>
                    </div>
                    <div v-else-if="ishere('tengah_semester', '1') != true">
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/tengah_semester/1/add'">
                        <div class="kotak kotak-hijau"></div>
                      </a>
                    </div>
                  </td>
                </tr>

                <tr>
                  <td class="text-center">1</td>
                  <td class="text-center">Akhir Semester 1</td>
                  <td class="text-center">
                    <div v-if="ishere('akhir_semester', 1) == true">
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/akhir_semester/1/detail'">
                        <div class="kotak kotak-pink">
                          <ion-icon src="assets/icon/view-icon.svg" class="text-center m-auto"></ion-icon>
                        </div>
                      </a>
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/akhir_semester/1/edit'">
                        <div class="kotak kotak-kuning">
                          <ion-icon src=""></ion-icon>
                        </div>
                      </a>
                      <a @click="delRapot('akhir_semester', 1)">
                        <div class="kotak kotak-merah">
                          <ion-icon src=""></ion-icon>
                        </div>
                      </a>
                    </div>
                    <div v-else-if="ishere('akhir_semester', '1') != true">
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/akhir_semester/1/add'">
                        <div class="kotak kotak-hijau"></div>
                      </a>
                    </div>
                  </td>
                </tr>

                <tr>
                  <td class="text-center">3</td>
                  <td class="text-center">Tengah Semester 2</td>
                  <td class="text-center">
                    <div v-if="ishere('tengah_semester', 2) == true">
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/tengah_semester/2/detail'">
                        <div class="kotak kotak-pink">
                          <ion-icon src="assets/icon/view-icon.svg" class="text-center m-auto"></ion-icon>
                        </div>
                      </a>
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/tengah_semester/2/edit'">
                        <div class="kotak kotak-kuning">
                          <ion-icon src=""></ion-icon>
                        </div>
                      </a>
                      <a @click="delRapot('tengah_semester', 2)">
                        <div class="kotak kotak-merah">
                          <ion-icon src=""></ion-icon>
                        </div>
                      </a>
                    </div>
                    <div v-else-if="ishere('tengah_semester', '2') != true">
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/tengah_semester/2/add'">
                        <div class="kotak kotak-hijau"></div>
                      </a>
                    </div>
                  </td>
                </tr>

                <tr>
                  <td class="text-center">4</td>
                  <td class="text-center">Akhir Semester 2</td>
                  <td class="text-center">
                    <div v-if="ishere('akhir_semester', 2) == true">
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/akhir_semester/1/detail'">
                        <div class="kotak kotak-pink">
                          <ion-icon src="assets/icon/view-icon.svg" class="text-center m-auto"></ion-icon>
                        </div>
                      </a>
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/akhir_semester/2/edit'">
                        <div class="kotak kotak-kuning">
                          <ion-icon src=""></ion-icon>
                        </div>
                      </a>
                      <a @click="delRapot('akhir_semester', 2)">
                        <div class="kotak kotak-merah">
                          <ion-icon src=""></ion-icon>
                        </div>
                      </a>
                    </div>
                    <div v-else-if="ishere('akhir_semester', '2') != true">
                      <a :href="'/pages/Rapor/' + tahun + '/' + kelas + '/' + id_siswa + '/akhir_semester/2/add'">
                        <div class="kotak kotak-hijau"></div>
                      </a>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>

          <!-- <nav aria-label="Page navigation example">
                        <ul class="pagination">
                            <li class="page-item"><a class="page-link" href="#">Previous</a></li>
                            <li class="page-item"><a class="page-link" href="/pages/Sarpras/DetailSarpras">1</a></li>
                            <li class="page-item"><a class="page-link" href="#">2</a></li>
                            <li class="page-item"><a class="page-link" href="#">3</a></li>
                            <li class="page-item"><a class="page-link" href="#">Next</a></li>
                        </ul>
                    </nav> -->
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useRouter } from "vue-router";
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
    IonCardHeader,
    // IonSearchbar
  },
  props: ["tahun", "kelas", "id_siswa"],
  data() {
    return {
      username: localStorage.getItem("username"),
      is_admin: localStorage.getItem("is_admin"),
      results: [],
    };
  },
  mounted: function () {
    let headers = {
      Authorization: "Bearer " + localStorage.getItem("access_token"),
    };

    axios
      .get("http://31.187.72.73:81/API/rapor/" + this.id_siswa, { headers })
      .then((response) => {
        this.results = response.data.rapor;
        this.results.nama_peserta_didik = response.data.nama_peserta_didik;
        console.log(response);
      })
      .catch(function (error) {
        console.error(error.response.data);
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

    ishere(periode, semester) {
      var res = false;
      this.results.forEach((element) => {
        if (element.periode == periode && element.semester == semester) {
          res = true;
        }
      });

      return res;
    },

    delRapot(semester, periode) {
      let headers = {
        Authorization: "Bearer " + localStorage.getItem("access_token"),
      };

      axios
        .delete("http://31.187.72.73:81/API/rapor/detail/" + this.id_siswa + "/" + semester + "/" + periode, { headers })
        .then((response) => {
          console.log(response);
          window.location.reload();
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

/* .table {
    border-collapse: inherit;
} */

thead th {
  padding: 0.75rem 1rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  border-bottom: 1px solid lighten(black, 35%);
}

th {
  font-weight: bold;
}

td,
th {
  white-space: nowrap;
}

.tables> :not(:last-child)> :last-child>* {
  border-bottom-color: black;
}

td {
  width: 100px;
}

.tambah {
  background: linear-gradient(135deg, #3a416f 0%, #141727 100%);
  border-radius: 8px;
  border: none;
  font-weight: bold;
}

.slide-custom-body {
  margin-top: 20px;
}

.slide-custom {
  width: 90%;
  margin: auto;
  border-radius: 18px;
}

.slide-custom img {
  width: 90%;
  max-height: 300px;
  object-fit: cover;
}

.card-content {
  margin: 30px 50px;
}

.card-content-judul {
  background: linear-gradient(135deg, #336b87 0%, #90afc5 100%);
  font-weight: bold;
  border-radius: 20px;
}

.card-content-judul:hover {
  background: linear-gradient(135deg, #90afc5 0%, #336b87 100%);
  transition: 5s ease-in;
  cursor: pointer;
}

.kotak {
  background-color: #141727;
  border-radius: 5px;
  width: 20px;
  height: 20px;
  display: inline-block;
  margin-right: 10px;
}

.kotak-pink {
  background-color: #f409f9;
}

.kotak-kuning {
  background-color: #f9f409;
}

.kotak-merah {
  background-color: #f90909;
}

.kotak-hijau {
  background-color: #09f909;
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
