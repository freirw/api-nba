<template>
    <div>
      <h2>Detalhes sobre o Time:</h2> 
      <div class="team-info">
        <p>Nome Completo do Time: {{ team.full_name }}</p>
        <p>Abreviação do Time: {{ team.abbreviation }}</p>
        <p>Cidade do Time: {{ team.city }}</p>
        <p>Liga do Time: {{ team.conference }}</p>
        <p>Divisão do Time: {{ team.division }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        team: {},
      };
    },
    created() {
     
      const teamId = this.$route.params.id;
      this.fetchTeamDetails(teamId);
    },
    methods: {
      async fetchTeamDetails(teamId) {
        try {
          const response = await fetch(`https://www.balldontlie.io/api/v1/teams/${teamId}`);
          if (response.ok) {
            const data = await response.json();
            this.team = data;
          } else {
            console.error('Erro ao buscar detalhes do time da NBA');
          }
        } catch (error) {
          console.error('Erro ao buscar detalhes do time da NBA', error);
        }
      },
    },
  };
  </script>
  
<style>
.team-info{
  color: white;
  font-family: 'Mooli-Regular', sans-serif; 
  margin-left: 20px;
}

h2{
  margin-top: 30px;
  margin-left: 20px;
  color: white;
  font-family: 'Mooli-Regular', sans-serif;
}
</style>