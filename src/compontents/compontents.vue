<template>
	<div>
		<h1>This Is Compontents</h1>
<h2>{{msg}}</h2>
<h1>{{msgs}}</h1>
<button @click='add'>add</button>
	</div>

</template>
<script type="text/javascript">
	export default {
		data(){
			return {
				msg:'this is msg'
			}
			
		},
		props:['msgs'],
		methods:{
			add(){
				this.$emit('myevent',this.msg)
			}
		}
	}


</script>