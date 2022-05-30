<template>
<!-- Main Wrapper -->
				<div id="main-wrapper">
					<div class="wrapper style2">
						<div class="inner">
							<div class="container">
								<div id="content">

									<!-- Content -->
										<article>
											<header class="major">
												<h2>Ma Collection</h2>
											</header>
											<!-- Je crée une boucle for qui va me permettre d'afficher les 3 cartes qui se trouvent sur la home page -->
											<div class='card-list' v-for="(card, index) in cards" :key="index">
												<!--Correspond à l'id de la carte, son titre et le bouton pour voir plus de détails -->
												<div class='card-title'><b>#{{index+1}} </b>{{card.name}}</div>
												<div style="cursor :pointer" class='card-action' @click="goToDetails(card.id)">👀</div>
											</div>	
										</article>
								</div>
							</div>
						</div>
					</div>
				</div>
</template>
<script>



import axios from 'axios';

const MAGIC_ALL_API_URL = "https://api.magicthegathering.io/v1/cards "

export default {
    name: 'CollectionView',
    data: () => ({
        cards: [] //array?????
    }), 
    components:{},
    methods: {
        goToDetails(id) {
            this.$router.push({ name: 'details', params: { cardId: id } })  //name of this is 
        }   
    },

    async created() {
		//On va chercher avec Get les DATA DE l'API pour toutes les cards
        const cards = await axios.get(MAGIC_ALL_API_URL)
		//console.log(cardsApi);
        //Axios renvoie les Data pour toutes les cards
        this.cards = cards.data.cards     
		//console.log(this.cards);
    }

};

</script>