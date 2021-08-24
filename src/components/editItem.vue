<template>
	<div class="edit" v-if="item">
		<h4>Edit Task</h4>
		<form class="wrapper">
			<p class="width-100 flex justify-content-between">
				<span class="">Title: </span>
				<input type="text"
							 v-model="item.title"
							 class="border-bottom margin-left width-100"></p>
			<p class="width-100 flex margin-top">
				<span>	Task: </span>
				<input type="text"
							 v-model="item.task"
							 class="border-bottom margin-left width-100">
			</p>
			<p class="width-100 flex margin-top align-item-center">
				<span>	Complete: </span>
				<input type="checkbox"
							 v-model="item.checked"
							 class="checkbox margin-left">
			</p>
			<div class="margin-top">
				<button class="btn-rounded" @click.prevent="handleConfirm">Save</button>
				<button class="btn-rounded margin-left" @click.prevent="handleCancel">Cancel</button>
			</div>
		</form>
	</div>
</template>

<script>
  export default {
    name: "editItem",
    props: ['item'],
    methods: {
      handleCancel() {
        this.$emit('action', false)
      },
      handleConfirm() {
        this.$emit('action', true)
      }
    }
  }
</script>
