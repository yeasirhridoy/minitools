<script setup>
const textToCompare = ref('')
const textToCompareWith = ref('')

const output = computed(() => {
  return diffString(textToCompare.value, textToCompareWith.value)
})

const diffString = (o, n) => {
  o = o.replace(/\s+$/, '');
  n = n.replace(/\s+$/, '');
  let out = diff(o === "" ? [] : o.split(/\s+/), n === "" ? [] : n.split(/\s+/));
  let str = "";
  let oSpace = o.match(/\s+/g);
  if (oSpace == null) {
    oSpace = ["\n"];
  } else {
    oSpace.push("\n");
  }
  let nSpace = n.match(/\s+/g);
  if (nSpace == null) {
    nSpace = ["\n"];
  } else {
    nSpace.push("\n");
  }
  if (out.n.length === 0) {
    for (let i = 0; i < out.o.length; i++) {
      str += '<del style="color: red;">' + escape(out.o[i]) + oSpace[i] + "</del>";
    }
  } else {
    if (out.n[0].text == null) {
      for (n = 0; n < out.o.length && out.o[n].text == null; n++) {
        str += '<del style="color: red;">' + escape(out.o[n]) + oSpace[n] + "</del>";
      }
    }
    for (let i = 0; i < out.n.length; i++) {
      if (out.n[i].text == null) {
        str += escape(out.n[i]) + nSpace[i];
      } else {
        let pre = "";
        for (n = out.n[i].row + 1; n < out.o.length && out.o[n].text == null; n++) {
          pre += '<del style="color: red;">' + escape(out.o[n]) + oSpace[n] + "</del>";
        }
        str += "<span style='color: #82ef17;'>" + out.n[i].text  + '</span>' + nSpace[i] + pre;
      }
    }
  }
  return str;
}

const diff = (o, n) => {
  let ns = {};
  let os = {};
  for (let i = 0; i < n.length; i++) {
    if (ns[n[i]] == null)
      ns[n[i]] = {rows: [], o: null};
    ns[n[i]].rows.push(i);
  }
  for (let i = 0; i < o.length; i++) {
    if (os[o[i]] == null)
      os[o[i]] = {rows: [], n: null};
    os[o[i]].rows.push(i);
  }
  for (let i in ns) {
    if (ns[i].rows.length === 1 && typeof (os[i]) != "undefined" && os[i].rows.length === 1) {
      n[ns[i].rows[0]] = {text: n[ns[i].rows[0]], row: os[i].rows[0]};
      o[os[i].rows[0]] = {text: o[os[i].rows[0]], row: ns[i].rows[0]};
    }
  }
  for (let i = 0; i < n.length - 1; i++) {
    if (n[i].text != null && n[i + 1].text == null && n[i].row + 1 < o.length && o[n[i].row + 1].text == null &&
        n[i + 1] === o[n[i].row + 1]) {
      n[i + 1] = {text: n[i + 1], row: n[i].row + 1};
      o[n[i].row + 1] = {text: o[n[i].row + 1], row: i + 1};
    }
  }
  for (let i = n.length - 1; i > 0; i--) {
    if (n[i].text != null && n[i - 1].text == null && n[i].row > 0 && o[n[i].row - 1].text == null &&
        n[i - 1] === o[n[i].row - 1]) {
      n[i - 1] = {text: n[i - 1], row: n[i].row - 1};
      o[n[i].row - 1] = {text: o[n[i].row - 1], row: i - 1};
    }
  }
  return {o: o, n: n};
}
</script>

<template>
  <div class="grid">
    <div class="col-12">
      <div class="card">
        <h1>Sentence Comparator</h1>
        <p>Compare two sentences and see the differences.</p>
        <div class="grid gap-2">
          <div class="col-12">
            <div class="flex-auto">
              <label for="textToCompare" class="font-bold mb-2">Text to compare</label>
              <Textarea id="textToCompare" v-model="textToCompare" auto-resize autofocus rows="10" class="w-full mt-2"
                        placeholder="Enter text to compare"/>
            </div>
          </div>
          <div class="col-12">
            <div class="flex-auto">
              <label for="textToCompareWith" class="font-bold mb-2">Text to compare with</label>
              <Textarea id="textToCompareWith" v-model="textToCompareWith" auto-resize autofocus rows="10"
                        class="w-full mt-2" placeholder="Enter text to compare with"/>
            </div>
          </div>
          <div class="col-12">
            <h4>Output</h4>
            <div class="mt-2 border-1 border-round border-gray-300 p-2 overflow-auto"
                 style="min-height: 64px;white-space:pre-wrap;">
              <HtmlParser :text="output"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>