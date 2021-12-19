<template>
      <svg>
      <polygon stroke="#07F9FE" stroke-width="2" fill="none" points="0,32 0,52 200,52 220,32 220,12 20,12"></polygon>
		<foreignObject x="20" y="22" width="100" height="20">
			<input v-bind:type="type" v-bind:placeholder="plc">
		</foreignObject>
      </svg>
</template>

<script>
	export default{
		props: ['type', 'plc'],
		
	}
</script>

<style>
	.field{
  display: inline;
  text-align: center;
}
svg {
  width: 250px;
  height: 60px;
}

input {
	outline: none;
	border: none;
	background: none;
  text-align: left;
  color: #07F9FE;
}
</style>
