<template>
  <div class="hello">
		<pdf
			ref="myPdfComponent"
			src="./static/1.pdf"
		></pdf>
  </div>
</template>

<script>
import pdf from 'vue-pdf'

export default {
  name: 'PDFViewer',
  components: {
    pdf
  },
  data () {
    return {

    }
  },

  mounted () {
    this.load()
  },
  methods: {
    load: function () {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>