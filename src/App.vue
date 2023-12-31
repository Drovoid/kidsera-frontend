<template>
  <ion-app>
    <ion-split-pane content-id="main-content" :disabled="disabledVariable">
      <ion-menu content-id="main-content" type="overlay" swipeEnabled="false" swipe-gesture="false">
        <ion-content>
          <ion-list id="inbox-list">
            <ion-row>
              <ion-col size="3"><img src="assets/img/kidsera-logo.png" alt="" style="width: 60px; padding: 0;"></ion-col>
              <ion-col size="9"><ion-list-header style="margin-top: 12px; padding: 0;">Kidsera Dashboard</ion-list-header></ion-col>
            </ion-row>
            <ion-note></ion-note>
            <ion-menu-toggle auto-hide="false" v-for="(p, i) in appPages" :key="i">
              <ion-item @click="selectedIndex = i" router-direction="root" :router-link="p.url" lines="none" detail="false" class="hydrated" :class="{ selected: selectedIndex === i }">
                <ion-icon slot="start" :ios="p.iosIcon" :md="p.mdIcon"></ion-icon>
                <ion-label>{{ p.title }}</ion-label>
              </ion-item>
            </ion-menu-toggle>
          </ion-list>
        </ion-content>
      </ion-menu>
      <ion-router-outlet id="main-content"></ion-router-outlet>
    </ion-split-pane>
  </ion-app>
</template>

<script lang="ts">
import { IonApp, IonContent, IonIcon, IonItem, IonLabel, IonList, IonListHeader, IonMenu, IonMenuToggle, IonNote, IonRouterOutlet, IonSplitPane } from '@ionic/vue';
import { defineComponent, ref } from 'vue';
import { useRoute } from 'vue-router';
import { archiveOutline, archiveSharp, bookmarkOutline, bookmarkSharp, heartOutline, heartSharp, mailOutline, mailSharp, paperPlaneOutline, paperPlaneSharp, trashOutline, trashSharp, warningOutline, warningSharp } from 'ionicons/icons';

export default defineComponent({
  name: 'App',
  data() {
    if (window.location.pathname == '/SignUp' || window.location.pathname == '/SignIn') {
      return {
        disabledVariable: true,
      };
    }
  },
  components: {
    IonApp, 
    IonContent, 
    IonIcon, 
    IonItem, 
    IonLabel, 
    IonList, 
    IonListHeader,
    IonMenu,
    IonMenuToggle,
    IonNote,
    IonRouterOutlet,
    IonSplitPane,
  },
  setup() {
    const selectedIndex = ref(0);
    const appPages = [
      {
        title: 'Home',
        url: '/pages/Dashboard',
        iosIcon: 'assets/icon/home.svg',
        mdIcon: 'assets/icon/home.svg'
      },
      {
        title: 'Peserta Didik',
        url: '/pages/PesertaDidik',
        iosIcon: 'assets/icon/pesertadidik-icon.svg',
        mdIcon: 'assets/icon/pesertadidik-icon.svg'
      },
      {
        title: 'Guru & Tenaga Kependidikan',
        url: '/pages/TenagaKependidikan',
        iosIcon: 'assets/icon/guru-icon.svg',
        mdIcon: 'assets/icon/guru-icon.svg',
      },
      {
        title: 'Sarana & Prasarana',
        url: '/pages/Sarpras',
        iosIcon: 'assets/icon/sapras-icon.svg',
        mdIcon: 'assets/icon/sapras-icon.svg'
      },
      {
        title: 'Rombongan Belajar',
        url: '/pages/RombonganBelajar',
        iosIcon: 'assets/icon/rombel-icon.svg',
        mdIcon: 'assets/icon/rombel-icon.svg'
      },
      {
        title: 'E - Rapor',
        url: '/pages/Rapor',
        iosIcon: 'assets/icon/rapor-icon.svg',
        mdIcon: 'assets/icon/rapor-icon.svg'
      },
    ];
    
    const path = window.location.pathname.split('pages/')[1];
    if (path !== undefined) {
      selectedIndex.value = appPages.findIndex(page => page.title.toLowerCase() === path.toLowerCase());
    }
    
    const route = useRoute();
    
    return { 
      selectedIndex,
      appPages, 
      archiveOutline, 
      archiveSharp, 
      bookmarkOutline, 
      bookmarkSharp, 
      heartOutline, 
      heartSharp, 
      mailOutline, 
      mailSharp, 
      paperPlaneOutline, 
      paperPlaneSharp, 
      trashOutline, 
      trashSharp, 
      warningOutline, 
      warningSharp,
      
      isSelected: (url: string) => url === route.path ? 'selected' : ''
    }
  }
});
</script>

<style scoped>
ion-menu ion-content {
  --background: var(--ion-item-background, var(--ion-background-color, #fff));
}

ion-menu.md ion-content {
  --padding-start: 8px;
  --padding-end: 8px;
  --padding-top: 20px;
  --padding-bottom: 20px;
}

ion-menu.md ion-list {
  padding: 20px 0;
}

ion-menu.md ion-note {
  margin-bottom: 30px;
}

ion-menu.md ion-list-header,
ion-menu.md ion-note {
  padding-left: 10px;
}

/* ion-menu.md ion-list#inbox-list {
  border-bottom: 1px solid var(--ion-color-step-150, #d7d8da);
} */

ion-menu.md ion-list#inbox-list ion-list-header {
  font-size: 22px;
  font-weight: 600;
  min-height: 20px;
}

ion-menu.md ion-item {
  --padding-start: 10px;
  --padding-end: 10px;
  border-radius: 4px;
}

ion-menu.md ion-item.selected {
  --background: rgba(var(--ion-color-primary-rgb), 0.14);
}

ion-menu.md ion-item.selected ion-icon {
  color: #fff;
  background-color: #1fbff1;
}

ion-menu.md ion-item ion-icon {
  color: #3a416f;
  padding: 5px;
  border-radius: 8px;
  background-color: white;
  box-shadow: 0px 4px 6px -1px rgba(0, 0, 0, 0.12), 0px 2px 4px -1px rgba(0, 0, 0, 0.07);
}

ion-menu.md ion-item ion-label {
  font-weight: 500;
}

ion-menu.ios ion-content {
  --padding-bottom: 20px;
}

ion-menu.ios ion-list {
  padding: 20px 0 0 0;
}

ion-menu.ios ion-note {
  line-height: 24px;
  margin-bottom: 20px;
}

ion-menu.ios ion-item {
  --padding-start: 16px;
  --padding-end: 16px;
  --min-height: 50px;
}

ion-menu.ios ion-item.selected ion-icon {
  color: var(--ion-color-primary);
}

ion-menu.ios ion-item ion-icon {
  font-size: 24px;
  color: #73849a;
}

ion-menu.ios ion-list-header,
ion-menu.ios ion-note {
  padding-left: 16px;
  padding-right: 16px;
}

ion-menu.ios ion-note {
  margin-bottom: 8px;
}

ion-note {
  display: inline-block;
  font-size: 16px;
  color: var(--ion-color-medium-shade);
}

ion-item.selected {
  --color: var(--ion-color-primary);
}

@media only screen and (min-width: 1440px) {
  ion-split-pane{
    --side-width: 335px;
  }
}

ion-col{
  padding: 0;
}
</style>
