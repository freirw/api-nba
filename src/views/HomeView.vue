<template>
  <div>
    <h1>Bem Vindo aos Times da NBA</h1>
    <ul class="team-list">
      <li v-for="(team, index) in displayedTeams" :key="index" class="team-item">
        <div class="team-card">
          <img :src="team.logoSrc" :alt="team.full_name" />
          <div class="team-infos">
            <p class="team-name">{{ team.full_name }}</p>
            <router-link :to="'/team/' + team.id" class="detalhes">Detalhes</router-link>
          </div>
        </div>
      </li>
    </ul>
    <button @click="anterior" :disabled="currentPage === 0" class="ajuste">Página Anterior</button>
    <button @click="proxima" :disabled="currentPage === maxPage" class="ajuste">Próxima Página</button>

  </div>
</template>

<script>
export default {
  data() {
    return {
      teams: [],
      currentPage: 0,
      itemsPerPage: 15,
      teamLogos: {
        'Atlanta Hawks': 'Atlanta Hawks.png',
        'Boston Celtics': 'Boston Celtics.jpg',
        'Brooklyn Nets': 'Brooklyn Nets.png',
        'Charlotte Hornets': 'Charlotte Hornets.png',
        'Chicago Bulls': 'Chicago Bulls.png',
        'Cleveland Cavaliers': 'Cleveland Cavaliers.png',
        'Dallas Mavericks': 'Dallas Mavericks.jpg',
        'Denver Nuggets': 'Denver Nuggets.jpg',
        'Detroit Pistons': 'Detroit Pistons.png',
        'Golden State Warriors': 'Golden State Warriors.webp',
        'Houston Rockets': 'Houston Rockets.png',
        'Indiana Pacers': 'Indiana Pacers.png',
        'LA Clippers': 'LA Clippers.png',
        'Los Angeles Lakers': 'Los Angeles Lakers.webp',
        'Memphis Grizzlies': 'Memphis Grizzlies.webp',
        'Miami Heat': 'Miami Heat.png',
        'Milwaukee Bucks': 'Milwaukee Bucks.png',
        'Minnesota Timberwolves': 'Minnesota Timberwolves.jpg',
        'New Orleans Pelicans': 'New Orleans Pelicans.png',
        'New York Knicks': 'New York Knicks.png',
        'Oklahoma City Thunder': 'Oklahoma City Thunder.jpg',
        'Orlando Magic': 'Orlando Magic.png',
        'Philadelphia 76ers': 'Philadelphia 76ers.png',
        'Phoenix Suns': 'Phoenix Suns.png',
        'Portland Trail Blazers': 'Portland Trail Blazers.png',
        'Sacramento Kings': 'Sacramento Kings.png',
        'San Antonio Spurs': 'San Antonio Spurs.png',
        'Toronto Raptors': 'Toronto Raptors.png',
        'Utah Jazz': 'Utah Jazz.png',
        'Washington Wizards': 'Washington Wizards.png',
      },
    };
  },
  computed: {
    maxPage(){
      return Math.ceil(this.teams.length / this.itemsPerPage) - 1;
    },
    displayedTeams() {
      const startIndex = this.currentPage * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.teams.slice(startIndex, endIndex);
  },
},
  methods: {
    async fetchNbaTeams() {
      try {
        const response = await fetch('https://www.balldontlie.io/api/v1/teams');
        if (response.ok) {
          const data = await response.json();

          const teamsWithLogos = data.data.map(team => ({...team,
            logoSrc: `public/img/${this.teamLogos[team.full_name]}` || '',
          }));

          this.teams = teamsWithLogos;
        } else {
          console.error('Erro ao tentar carregar times da NBA');
        }
      } catch (error) {
        console.error('Erro ao tentar carregar times da NBA', error);
      }
    },
    
    anterior() {
      if (this.currentPage > 0) {
        this.currentPage--;
      }
    },
    proxima() {
      if (this.currentPage < this.maxPage) {
        this.currentPage++;
      }
    },
},
  created() {
    this.fetchNbaTeams();
  },
};
</script>

<style>
h1{
  font-family: 'Mooli-Regular', sans-serif;
  font-size: 50px;
  text-align: center;
  margin-top: 20px;
  color:#7693e2;
  font-weight: bolder;
}

.team-list {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding: 5;
  margin: 5;
  margin-top: 10rem;
}

.team-item {
  flex: 0 0 calc(25% - 10px);
  margin: 5px;
  box-sizing: border-box;
}

.team-card {
  border: 1px solid #ccc;
  padding: 15px;
  background-color: #f9f9f9;
  border-radius: 5px;
  display: flex;
  align-items: center;
  max-width: 100%;
  box-sizing: border-box;
  overflow: hidden;


}

.team-card img {
  max-width: 100px;
  max-height: 100px;
  margin-right: 10px;
}


.team-name {
  font-family: 'Mooli-Regular', sans-serif;
  font-size: 20px;
}

.detalhes{
  text-decoration: none;
  display: inline-block;
  padding: 5px 10px;
  border-radius: 5px;  
  color: #333;
  font-weight: bolder; 
  background-color: #7e9fca;
}
.ajuste{
  display:flex;
  text-align: center;
  padding: 5px 10px;
  border-radius: 5px;  
  color: #333;
  font-weight: bolder; 
  background-color: #7e9fca;
  justify-content: center; 
  margin-top: 20px;
  margin-left: 62rem;
}
</style>
