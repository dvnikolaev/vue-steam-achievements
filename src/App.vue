<template>
  <div id="app">
    <AppForm
      :err="steamData.err"
      @update:inputValue="updateSteamData"
      @update:spinner="switchSpinner"
      @update:listOfGames="downloadListOfGames"
      v-if="showForm"/>
    <AppListGames 
      :listOfGames="listOfGames"
      :activeGameName="activeGame.name"
      @update:activeGame="updateActiveGame"
      v-if="listOfGames.length"/>
    <AppSpinner v-if="showSpinner" />
    <Notification :text="notificationText"/>
    <AppListAchievements :activeGame="activeGame" />
  </div>
</template>

<script>
import axios from "axios";

import AppSpinner from "./components/AppSpinner";
import AppListAchievements from "./components/AppListAchievements";
import AppListGames from "./components/AppListGames"
import AppForm from "./components/AuthForm/AppForm";
import Notification from "./components/Notification";

export default {
  name: "App",
  data() {
    return {
      steamData: {
        apiKey: '',
        steamId: '',
        loading: false,
        err: ''
      },
      listOfGames: [],
      activeGame: {
        name: '',
        achievements: [],
        hiddenAchievements: [],
        loading: null
      },
      notificationText: ''
    }
  },
  computed: {
    showForm() {
      return !this.listOfGames.length && !this.steamData.loading ? true : false;
    },
    showSpinner() {
      return !this.listOfGames.length && this.steamData.loading ? true : false;
    }
  },
  methods: {
    updateSteamData(value, key) {
      this.steamData[key] = value;
    },
    switchSpinner() {
      console.log(`switchSpinner`);
      this.steamData.loading = !this.steamData.loading;
    },
    async downloadListOfGames(games) {
      if (this.steamData.apiKey && this.steamData.steamId) {
        this.steamData.loading = true;

        try {
          // Получаем список игр аккаунта
          let {data: { response: { games } }} = await axios.get(`${process.env.VUE_APP_STEAM_API_URL}IPlayerService/GetOwnedGames/v0001/?key=${this.steamData.apiKey}&steamid=${this.steamData.steamId}&format=json&include_appinfo=true&include_played_free_games=true`);  
          this.listOfGames = games;
          this.steamData.loading = false;
        } catch(err) {
          console.log(err);
          switch (err.response.status) {
            case 401: // Если неверный Steam API KEY
              console.log(this.steamData);
              this.steamData.err = 'Ошибка! Проверьте правильность вашего Steam API KEY';
              break;
            case 500: // Если неверный Steam ID
              this.steamData.err = 'Ошибка! Проверьте правильность вашего Steam ID';
              break;
            case 403: // Если Аккаунт закрыт или открыт только для друзей
              this.steamData.err = 'Ошибка! Необходимо сделать аккаунт видимым для всех';
              break;
            default:
              this.steamData.err = `Ошибка! Попробуйте позже`;
              break;
          }
          this.steamData.loading = false;
        }
      }
    },
    async updateActiveGame(id, name) {
      this.activeGame.loading = true;
      this.activeGame.hiddenAchievements = [];
      this.activeGame.achievements = [];
      
      try {
        let { data: { playerstats: { achievements: achivedFlagArray }}} = await axios.get(`${process.env.VUE_APP_STEAM_API_URL}ISteamUserStats/GetPlayerAchievements/v0001/?appid=${id}&key=${this.steamData.apiKey}&steamid=${this.steamData.steamId}&l=russian`);
        let { data: { game: { availableGameStats: { achievements: achievementsArray }}}} = await axios.get(`${process.env.VUE_APP_STEAM_API_URL}ISteamUserStats/GetSchemaForGame/v2/?key=${this.steamData.apiKey}&appid=${id}&l=russian`);
      
        let achievements = achievementsArray.map((item, i) => {
          return {
            name: item.name,
            displayName: item.displayName,
            description: item.description,
            icon: item.icon,
            hidden: item.hidden,
            achieved: achivedFlagArray[i].achieved
          }
        });

        if(achievements.every(item => item.achieved)) {
          this.notificationText = "Вы получили все достижения в данной игре!"
          this.activeGame.loading = false;

          setTimeout(() => {
            this.notificationText = '';
          },1000)

          return;
        }
        
        this.activeGame.hiddenAchievements = achievements.filter(item => !item.achieved && item.hidden);
        this.activeGame.achievements = achievements.filter(item => !item.achieved && !item.hidden);
        this.activeGame.name = name;
        this.activeGame.loading = false;
      } catch(err) {
        console.log(err);
        this.activeGame.loading = false;
        if (err.response.status === 400) {
          this.notificationText = "У данной игры нет достижений!"

          setTimeout(() => {
            this.notificationText = '';
          },1000)
        }
      }
      

      
    }
  },
  components: {
    AppSpinner,
    AppListAchievements,
    AppListGames,
    AppForm,
    Notification
  }
};
</script>

<style>
body {
  background-color: #24282F;
  font-family: 'Montserrat', sans-serif;
}
#app {
  display: flex;
}

@media screen and (max-width: 1195px) {
  body {
    margin: 0;
  }
  #app {
    flex-direction: column;
  }
}
</style>