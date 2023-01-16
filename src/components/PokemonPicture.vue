<template lang="">
	<div class="container">
		<img :src="imgSrc" class="hidden" alt="pokemon" />
		<img :src="imgSrc" v-if="showPokemon" class="fade-in" alt="pokemon" />
	</div>
</template>
<script >
export default {
	props: {
		pokemonId: {
			type: Number,
			required: true,
		},
		showPokemon: {
			type: Boolean,
			required: true,
			default: false,
		},
	},
	computed: {
		imgSrc() {
			return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
		},
	},
};
</script>
<style lang="scss">
.hidden {
	filter: brightness(0);
}

.container {
	height: 200px;
}

.fade-in {
	animation: fadeIn 0.3s;
	-webkit-animation: fadeIn 0.3s;
	-moz-animation: fadeIn 0.3s;
	-o-animation: fadeIn 0.3s;
	-ms-animation: fadeIn 0.3s;
}

img {
	height: 200px;
	position: absolute;
	right: 40%;
	user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	-webkit-user-drag: none;
	-webkit-user-select: none;
}

@media screen and (max-width: 768px) {
	img {
		right: 30%;
	}
}

@media screen and (max-width: 480px) {
	img {
		right: 20%;
	}
}

@keyframes fadeIn {
	0% {
		opacity: 0;
	}

	100% {
		opacity: 1;
	}
}

@-moz-keyframes fadeIn {
	0% {
		opacity: 0;
	}

	100% {
		opacity: 1;
	}
}

@-webkit-keyframes fadeIn {
	0% {
		opacity: 0;
	}

	100% {
		opacity: 1;
	}
}

@-o-keyframes fadeIn {
	0% {
		opacity: 0;
	}

	100% {
		opacity: 1;
	}
}

@-ms-keyframes fadeIn {
	0% {
		opacity: 0;
	}

	100% {
		opacity: 1;
	}
}
</style>
