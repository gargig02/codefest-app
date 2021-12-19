<template>
	<form>
  		<div class="field_container">
    		<ul>
    			<li>
    				<div class="field"><box :plc="plc" :type="type">
    				</box></div>
    			</li>
    		</ul>
    	</div>
    </form>
</template>

<script>
	const box = () => import("@components/box");

	export default{
		components: {box,},
		data(){
			return {
				plc: 'Email',
				type: 'text',
			}
		}
	}
</script>