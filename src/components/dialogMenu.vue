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

<style scoped>
	.dialog {
		padding: 20px;
		border-radius: 20px;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		position: absolute;
		width: 50vw;
		height: 12vh;
		background: rgba(97, 86, 86, 0.4);
		z-index: 100;
		color: #fff;
	}

</style>