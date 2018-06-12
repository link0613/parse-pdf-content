<template>
  <div class="hello">
    <button @click="logContent()">
			getInfo
		</button>
    <div class="preview-pdf">
      <h2>fn</h2>
		  <pdf ref="myPdfComponent" :src="fn"></pdf>
    </div>
    <div class="result-data">
      <h2>Result</h2>
      <table>
        <tr>
          <th>Date</th>
          <th>Value date</th>
          <th>Ref. number</th>
          <th>Trans. Type</th>
          <th>Description</th>
          <th>Currency</th>
          <th>Debit</th>
          <th>Balance</th>
        </tr>
        <tr v-for="(row, index) in data" v-bind:key="index">
          <td>{{row.date}}</td>
          <td>{{row.valueDate}}</td>
          <td>{{row.refNumber}}</td>
          <td>{{row.transType}}</td>
          <td>{{row.description}}</td>
          <td>{{row.currency}}</td>
          <td>{{row.debit}}</td>
          <td>{{row.balance}}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import pdf from 'vue-pdf'

export default {
  /* eslint-disable */
  name: 'PDFViewer',
  components: {
    pdf
  },
  data () {
    return {
      fn: "https://bitcoin.org/bitcoin.pdf",
      data: []
    }
  },

  mounted () {
    this.load()
  },
  methods: {
    load: function () {

    },

    pushArray: function (rowData) {
      console.log(rowData)
      this.data.push(rowData)
    },

    logContent: function () {
      const vm = this
      
      this.$refs.myPdfComponent.pdf.forEachPage ( function (page) {
        
        return page.getTextContent()
        .then (function(content) {
          const text = content.items.map(item => item.str)
          console.log(text)
          const lenthOfWord = text.length
          for (let i = 0; i < lenthOfWord - 3; i++) {
            if (text[i].trim().length == 10 && 
              text[i + 1].trim().length == 10  
            ) {
              
              let j = 0
              let rowData 
              for (;;) {
                rowData = {}  
                rowData.date = text [ i + j++ ].trim()
                if (rowData.date.length !== 10) break
                rowData.valueDate = text [ i + j++ ]
                if (rowData.valueDate.length !== 10) break
                rowData.refNumber = text [ i + j++ ]
                rowData.transType = text [ i + j++ ]

                rowData.description = text [ i + j++ ]
                while (text [i + j].trim() !=='EUR' && text [i + j].trim() !=='USD') {
                  rowData.description += ' ' + text [ i + j++ ]
                }
           
                rowData.currency = text [ i + j++ ]
                rowData.debit = text [ i + j++ ]
                rowData.credit = text [ i + j++ ]
                rowData.balance = text [ i + j++ ]
                vm.pushArray(rowData)
              }
              i += j
            }
          }
        })
			})
		}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .preview-pdf {
    overflow-y: scroll;
    height: 400px;
    border: 1px solid;
  }
  table, th, td {
      border: 1px solid black;
      border-collapse: collapse;
  }
</style>