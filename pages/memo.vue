<template>
  <v-layout>
    <v-flex class="text-rigth">
      <h2>メモ新規登録</h2>
      <v-form ref='form' v-on:submit.prevent="createMemo(memo)">
        <v-text-field label="題名" required outlined v-model='memo.title' placeholder='題名を入力してください'></v-text-field>
        <v-textarea label="本文" required outlined rows="5" v-model='memo.body' placeholder='本文を入力してください'></v-textarea>
        <v-btn v-on:click.prevent="createMemo(memo)" color='primary'>新規登録</v-btn>
      </v-form>
      <hr>
      <h2>メモ一覧</h2>
      <v-data-table
        :headers="headers"
        :items="items"
        :items-per-page="5"
        class="elevation-1"
      >
      </v-data-table>
    </v-flex>
    <!-- 登録成功メッセージ -->
    <v-snackbar
      v-model="snackbar"
      :bottom="true"
      color="success"
      :multi-line="false"
      :right="true"
      :timeout="3000"
      :vertical="false"
    >
      新規登録しました
      <v-btn
        dark
        text
        @click="snackbar = false"
      >
        <v-icon>mdi-check</v-icon>
      </v-btn>
    </v-snackbar>
  </v-layout>
</template>

<script>
export default {
  data: function() {
    return {
      memo: {
        title: '',
        body: '',
      },
      headers: [
        {
          text: '題名',
          align: 'left',
          value: 'title',
        },
        { text: '本文', value: 'body' },
      ],
      items: [
        {title: '掃除', body: '部屋の掃除をする'},
        {title: '買い物', body: '夕食のおかずを買いに行く'},
      ],
      snackbar: false,
    }
  },
  methods: {
    createMemo: function() {
      this.items.push(this.memo)
      this.snackbar = true
      this.clear()
    },
    clear: function() {
      this.memo = {
        title: '',
        body: '',
      }
    },
  }
}
</script>

<style scoped>
hr {
  margin-top: 10px;
}
h2 {
  margin: 10px 0px;
}
</style>