<template>
  <div class="hello">
		<button
			@click="logContent"
		>
			log content
		</button>
		<pdf
			ref="myPdfComponent"
			src="https://cdn.mozilla.net/pdfjs/tracemonkey.pdf"
		></pdf>
  </div>
</template>

<script>
import pdf from 'vue-pdf'

export default {
  name: 'getPdfContent',
  components: {
		pdf
	},
  props: {
    fn: String
  },
	data() {
		return {
			content: ''
		}
	},
  methods: {
		logContent() {
      // eslint-disable-next-line 
      console.log('----', this.$refs.myPdfComponent.pdf)
			this.$refs.myPdfComponent.pdf.forEachPage(function(page) {
				return page.getTextContent()
				.then(function(content) {
					let text = content.items.map(item => item.str);
          // eslint-disable-next-line 
					console.log(text);
				})
			})

		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
