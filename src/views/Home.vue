<template>
	<div class="home">
		<div>
			<div>
				<b-button id="show-btn" @click="$bvModal.show('modal')">This button will trigger modal</b-button>

				<!-- Modal -->
				<b-modal size="lg" class="px-2 py-2" id="modal" hide-header hide-footer>
					<!-- Input form content -->
					<form>
						<b-row>
							<!-- Title -->
							<b-col cols="12">
								<h4>Add Revenue Group</h4>
							</b-col>

							<!-- Revenue group input -->
							<b-col class="mt-3" cols="12">
								<b-row>
									<b-col cols="12">
										<div>Revenue Group Title</div>
									</b-col>
									<b-col class="mt-1" cols="12">
										<b-form-input></b-form-input>
									</b-col>
								</b-row>
							</b-col>

							<!-- Dropdown -->
							<b-col class="mt-3" cols="12">
								<b-row>
									<b-col cols="12">
										if
										<span style="width: 20%">
											<select class="form-control d-inline-block w-25 mr-1">
												<option selected>All</option>
												<option value="1">im not selected</option>
											</select>
										</span>

										of the below condition are met
									</b-col>
								</b-row>
							</b-col>

							<!-- Rules -->
							<b-col class="mt-3 background" cols="12">
								<b-row v-for="(rule, index) in fields.rules" :key="index" class="py-3">
									<!-- first dropdown -->
									<b-col cols="2" class="pr-1">
										<select v-model="fields.rules[index].firstDropdown" class="form-control">
											<option selected value="">aff_sub</option>
											<option value="1">im not selected</option>
										</select>
									</b-col>

									<!-- second dropdown -->
									<b-col cols="2" class="px-1">
										<select v-model="fields.rules[index].secondDropdown" class="form-control">
											<option selected value="">aff_sub</option>
											<option value="1">im not selected</option>
										</select>
									</b-col>

									<!-- parameter input -->
									<b-col cols="8" v-for="(parameter, innerIndex) in fields.rules[index].parameters" :key="innerIndex">
										<b-row>
											<b-col cols="8" class="px-1">
												<b-input-group>
													<b-form-input cols="6" v-model="fields.rules[index].parameters[innerIndex]"></b-form-input>
													<b-input-group-append>
														<b-button
															@click="addParameters(index)"
															v-show="fields.rules[index].parameters.length - 1 === innerIndex"
															cols="2"
															variant="outline-primary"
															>add rule</b-button
														>
														<b-button
															@click="removeParameters(index, innerIndex)"
															v-show="fields.rules[index].parameters.length - 1 !== innerIndex"
															cols="2"
															variant="outline-danger"
															>remove rule</b-button
														>
													</b-input-group-append>
												</b-input-group>
											</b-col>

											<!-- Button -->
											<b-col cols="4" class="px-1 py-1">
												<!-- minus -->
												<b-button @click="removeRules(index)" variant="outline-*" :disabled="fields.rules.length === 1">
													<b-icon icon="dash-circle" style="width: 25px; height: 25px"></b-icon>
												</b-button>

												<!-- add -->
												<b-button variant="outline-*" @click="addRules()" :disabled="false">
													<b-icon style="width: 25px; height: 25px" icon="plus-circle"></b-icon>
												</b-button>
											</b-col>
										</b-row>
									</b-col>
								</b-row>
							</b-col>

							<!-- Total revenue -->
							<b-col class="mt-3" cols="12">
								<b-row>
									<b-col cols="12">
										<div>
											<b-input-group append="%" class="w-50">
												<div class="mr-1">then revenue is</div>
												<b-form-input readonly v-model="fields.totalRevenue.value"></b-form-input>
											</b-input-group>
										</div>
									</b-col>
								</b-row>
							</b-col>
						</b-row>

						<!-- Button -->
						<b-row class="mt-4">
							<b-col cols="12">
								<button type="button" class="btn btn-warning mr-1" block @click="confirm">Confirm</button>
								<button type="button" class="btn btn-secondary" block @click="$bvModal.hide('modal')">Cancel</button>
							</b-col>
						</b-row>
					</form>
				</b-modal>
			</div>
		</div>
	</div>
</template>

<script>
const name = 'Home'
const data = function data() {
	return {
		name,
		fields: {
			totalRevenue: {
				value: '15'
			},
			rules: [
				{
					firstDropdown: '',
					secondDropdown: '',
					parameters: ['']
				}
			]
		}
	}
}

const methods = {
	confirm() {
		this.$bvModal.hide('modal')
	},
	addRules() {
		const tempObj = {
			firstDropdown: '',
			secondDropdown: '',
			parameters: ['']
		}
		this.fields.rules.push(tempObj)
	},
	removeRules(index) {
		console.warn(index)
		this.fields.rules.splice(index, 1)
	},
	addParameters(index) {
		this.fields.rules[index].parameters.push('')
	},
	removeParameters(index, innerIndex) {
		console.warn(index, innerIndex)
	}
}

export default {
	name,
	data,
	components: {},
	methods
}
</script>

<style >
.background {
	background-color: #d3d3d3;
}
</style>
