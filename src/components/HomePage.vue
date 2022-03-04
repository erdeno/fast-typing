<template>
  <div class="container">
    <section class="hero is-warning">
      <div class="hero-body">
        <p class="title">Hızlı yazma yarışması</p>
        <p class="subtitle">Ne kadar hızlı klavye kullandığını test et.</p>
        <div>Doğru sayısı: {{ trueCount }} Yanlış sayısı: {{ falseCount }}</div>
        <div class="box mb-1">
          <span
            v-for="(word, key) in words"
            :key="key"
            class="ml-2 is-size-4"
            :class="key != 0 || writtenWordControl"
            >{{ word }}</span
          >
        </div>
        <div class="box">
          <div class="field is-grouped">
            <p class="control is-expanded">
              <input class="input" type="text" v-model="writtenWord" />
            </p>
            <p class="control">
              <a class="button is-static">1:00</a>
              <a class="button">reload</a>
            </p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "HomePage",
  data() {
    return {
      words: ["Elma", "Armut", "Portakal", "kiraz"],
      writtenWord: null,
      isTrue: true,
      trueCount: 0,
      falseCount: 0,
    };
  },
  watch: {
    writtenWord(val) {
      const word = this.words[0].slice(0, val.length);
      const userWord = val.replace(" ", "");
      this.isTrue = word == userWord;

      if (val.indexOf(" ") !== -1) {
        this.isTrue ? (this.trueCount += 1) : (this.falseCount += 1);
        this.words.splice(0, 1);
        this.writtenWord = "";
      }
    },
  },
  computed: {
    writtenWordControl() {
      return this.isTrue
        ? "written-word"
        : "written-word has-background-danger-dark";
    },
  },
};
</script>

<style>
.written-word {
  background-color: gray;
  color: white;
  padding: 0.3rem;
  border-radius: 0.3rem;
}
</style>
