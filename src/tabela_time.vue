<template>
	<div>
		<h1>Time: {{ time.nome }}</h1>
		<h1>Estado: {{ time.estado }}</h1>
		<h1>Descrição: {{ time.info }}</h1>
		<table class="table is-hoverable">
			<thead>
			<tr>
				<th>Nome</th>
				<th>Camisa</th>
				<th>Gols</th>
				<th>Posição</th>
				<th>Editar</th>
				<th>Apagar</th>
			</tr>
			</thead>
			<tbody>
			<tr v-for="jogador in jogadores">
				<td>{{ jogador.nome }}</td>
				<td>{{ jogador.camisa }}</td>
				<td>{{ jogador.gols }}</td>
				<td>{{ jogador.posicao }}</td>
				<td>
					<button class="button is-info" @click="editar_jogador(jogador)">editar</button>
				</td>
				<td>
					<span v-if="carregando" class="button is-loading">carregando</span>
					<button v-else class="button is-danger"
					        @click="actions_jogador_apagar(jogador)">apagar
					</button>
				</td>
			</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
import {mapState, mapGetters, mapActions} from 'vuex'

export default {
	name: 'tabela_time',
	computed: {
		...mapState(['jogadores', 'carregando']),
		...mapGetters(['pegarTime', 'pegarJogadores']),
		timeIdUrl() {
			return this.$route.params.id
		},
		time() {
			return this.pegarTime(this.timeIdUrl)
		},
		jogadores() {
			return this.pegarJogadores(this.timeIdUrl)
		}
	},
	methods: {
		...mapActions(['actions_jogador_apagar']),
		editar_jogador(jogador) {
			this.$bus.emit('editar_jogador', jogador)
		}
	}
}
</script>

<style>

</style>
