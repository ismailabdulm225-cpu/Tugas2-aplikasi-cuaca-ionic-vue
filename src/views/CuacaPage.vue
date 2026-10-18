<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Perkiraan Cuaca Di Jakarta</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Perkiraan Cuaca Di Jakarta</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-card v-for="item in weatherData" :key="item.time">
        <ion-card-header>
          <ion-card-title>
            {{ getWeatherEmoji(item.temp) }}
            {{ formatTemp(item.temp) }}
          </ion-card-title>

          <ion-card-subtitle> 🕐{{ formatTime(item.time) }} </ion-card-subtitle>
        </ion-card-header>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonContent,
  IonTitle,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardSubtitle,
} from "@ionic/vue";

import { ref, onMounted } from "vue";
import axios from "axios";

// Menyimpan data tempratur dan waktu
const weatherData = ref<any[]>([]);

// URL API Sesuai soal
const apiURL =
  "https://api.open-meteo.com/v1/forecast?latitude=-6.2&longitude=106.8&hourly=temperature_2m";

// Mengambil data ketika halaman dibuka
onMounted(() => {
  getWeatherData();
});

// Mengambil data dari API
const getWeatherData = async () => {
  try {
    const response = await axios.get(apiURL);
    const data = response.data;
    const times = data.hourly.time;
    const temps = data.hourly.temperature_2m;

    // Mengambil seluruh data
    weatherData.value = times.map((time: string, index: number) => {
      return {
        time,
        temp: temps[index],
      };
    });
  } catch (eror) {
    console.error("Gagal engambil data Cuaca", eror);
  }
};

// Mengubah format waktu dan tanggal
const formatTime = (time: string) => {
  const date = new Date(time);

  return date.toLocaleString("id-ID", {
    weekday: "long",
    day: "2-digit",
    month: "long",
    year: "numeric",
    hour: "2-digit",
    minute: "2-digit",
    timeZone: "Asia/Jakarta",
  });
};

// Menentukan simbol cuaca hanya simulasi (☀️🌧️🌦️🌥️)
const getWeatherEmoji = (temp: number): string => {
  if (temp <= 23) {
    return "🌧️";
  } else if (temp <= 27) {
    return "🌦️";
  } else if (temp <= 30) {
    return "🌥️";
  } else {
    return "☀️";
  }
};

// Mengubah format temperatur menjadi derajat celcius
const formatTemp = (temp: number) => {
  const t = Math.floor(temp);
  return `${t}°C`;
};
</script>

<style scoped>
ion-title {
  font-family: "Times New Roman", Times, serif;
  font-size: 30px;
  font-weight: 500px;
  letter-spacing: 0.5px;
  text-align: left;
  color: #fff;
}

ion-toolbar {
  --background: #252b30;
  --color: #ffffff;
}

ion-card {
  margin: 12px 16px;
  border-radius: 20px;
  background: #252b30;
  box-shadow: 0 4px 5px rgb(3, 253, 195);
  border-bottom: 3px solid #0619eb;
}

ion-card-title {
  font-size: 22px;
  font-weight: 600;
  color: #01c0ff;
}

ion-card-subtitle {
  margin-top: 8px;
  font-size: 14px;
  line-height: 1.5;
  color: #fff;
}
</style>
