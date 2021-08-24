<template>
	<div class="dialog">
		<h4>Are You Sure ?</h4>
		<div class="margin-top">
			<button class="btn-rounded" @click="handleYes">YES</button>
			<button class="btn-rounded margin-left" @click="handleNo">No</button>
		</div>
	</div>
</template>

<script>
  export default {
    name: "dialogMenu",
    methods: {
      handleYes() {
        this.$emit('confirm', true)
      },
      handleNo() {
        this.$emit('confirm', false)
      }
    }
  }
</script>
