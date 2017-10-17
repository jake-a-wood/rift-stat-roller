<template>
<v-layout column justify-center align-center>
	<v-flex xs12 sm8 md6>
		<v-card>
			<v-card-title  primary-title>
				<h3 class="headline mb-0">
					Click and roll stats!
				</h3>
			</v-card-title>
			<v-card-actions>
				<v-btn @click="onRollClick">
					ROLL
				</v-btn>
			</v-card-actions>
			<v-card-text>
				<div v-for="stats in rolls">
					<span v-for="stat in stats"
						:class="{bonus: stat > 15}">
						{{stat}},
					</span>
					<span class="total">
						{{stats.reduce((sum, value) => sum + value)}}
					</span>
				</div>
			</v-card-text>
		</v-card>
	</v-flex>
</v-layout>
</template>

<script>
export default {
	data () {
		return {
			rolls: []
		}
	},
	methods: {
		onRollClick () {
			this.rolls.push([0, 0, 0, 0, 0, 0, 0, 0].map(stat => {
				return this.roll3NoOnesPlusBonus()
			}))
		},

		roll () {
			return Math.round(Math.random() * (6 - 1) + 1)
		},

		rollNoOnes () {
			let roll = this.roll()
			return roll === 1 ? this.rollNoOnes() : roll
		},

		roll3NoOnes () {
			return this.rollNoOnes() + this.rollNoOnes() + this.rollNoOnes()
		},

		roll3NoOnesPlusBonus () {
			let stat = this.roll3NoOnes()
			return stat > 15 ? stat + this.roll() : stat
		}
	}
}
</script>

<style scoped>
.bonus {
	color: green;
	font-weight: bold;
}
.total {
	background-color: black;
	font-weight: bold;
}
</style>
