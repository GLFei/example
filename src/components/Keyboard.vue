<template>
  <div class="keyboard">
    <div class="keyboard-panel">
      <div class="key-part">
        <div
          class="key"
          v-for="(key, index) in keys"
          :key="index"
          :style="key.style"
        >
          {{ key.value }} {{ key.supKey }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Keywoard",
  data() {
    return {
      keys: [
        // ←↓↑→ ⇥
        { value: "`", supKey: "~" },
        { value: "1", supKey: "!" },
        { value: "2", supKey: "@" },
        { value: "3", supKey: "#" },
        { value: "4", supKey: "$" },
        { value: "5", supKey: "%" },
        { value: "6", supKey: "^" },
        { value: "7", supKey: "&" },
        { value: "8", supKey: "*" },
        { value: "9", supKey: "(" },
        { value: "0", supKey: ")" },
        { value: "-", supKey: "_" },
        { value: "=", supKey: "+" },
        { value: "←", style: { width: "103px" } },
        { value: "→", style: { width: "74px" } },
        { value: "Q", style: { "text-align": "left" } },
        { value: "W", style: { "text-align": "left" } },
        { value: "E", style: { "text-align": "left" } },
        { value: "R", style: { "text-align": "left" } },
        { value: "T", style: { "text-align": "left" } },
        { value: "Y", style: { "text-align": "left" } },
        { value: "U", style: { "text-align": "left" } },
        { value: "I", style: { "text-align": "left" } },
        { value: "O", style: { "text-align": "left" } },
        { value: "P", style: { "text-align": "left" } },
        { value: "[", supKey: "{" },
        { value: "]", supKey: "}" },
        { value: "\\", supKey: "|", style: { width: "74px" } },
        { value: "↓", style: { width: "89px" } },
        { value: "A", style: { "text-align": "left" } },
        { value: "S", style: { "text-align": "left" } },
        { value: "D", style: { "text-align": "left" } },
        { value: "F", style: { "text-align": "left" } },
        { value: "G", style: { "text-align": "left" } },
        { value: "H", style: { "text-align": "left" } },
        { value: "J", style: { "text-align": "left" } },
        { value: "K", style: { "text-align": "left" } },
        { value: "L", style: { "text-align": "left" } },
        { value: ";", supKey: ":" },
        { value: "'", supKey: '"' },
        { value: "↙", style: { width: "107px" } },
        { value: "↑", style: { width: "106px" } },
        { value: "Z", style: { "text-align": "left" } },
        { value: "X", style: { "text-align": "left" } },
        { value: "C", style: { "text-align": "left" } },
        { value: "V", style: { "text-align": "left" } },
        { value: "B", style: { "text-align": "left" } },
        { value: "N", style: { "text-align": "left" } },
        { value: "M", style: { "text-align": "left" } },
        { value: ",", supKey: "<" },
        { value: ".", supKey: ">" },
        { value: "/", supKey: "?" },
        { value: "↑", style: { width: "138px" } },
        { value: "Ctrl", style: { width: "57px" } },
        { value: "Win", style: { width: "57px" } },
        { value: "Alt", style: { width: "57px" } },
        { value: "", style: { width: "307px" } },
        { value: "Alt", style: { width: "57px" } },
        { value: "Fn", style: { width: "57px" } },
        { value: "▤", style: { width: "57px" } },
        { value: "Ctrl", style: { width: "57px" } },
      ],
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.keyboard {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.keyboard-panel {
  height: 310px;
  width: 764px;
  background-color: #888;
  border-radius: 8px;
  padding: 10px;
  border-top: 5px solid #a5a5a5;
  border-bottom: 42px solid #504e4e;
  border-right: 5px solid #9f9f9f;
  border-left: 5px solid #726f6f;
}

.key-part {
  display: flex;
  flex-wrap: wrap;
  background-color: #aaa;
  border: 2px inset #999;
}
.key {
  width: 45px;
  height: 45px;
  color: white;
  background-color: silver;
  line-height: 1;
  padding: 4px;
  border-radius: 7px;
  border-top: 3px #4c48481f;
  border-bottom: 8px #777;
  border-left: 5px #888;
  border-right: 5px #ddd;
  border-style: solid;
  margin-top: 1px;
  margin-bottom: 2px;
  margin-left: 1.5px;
  margin-right: 1.5px;
  font-size: 12px;
  user-select: none;
  text-align: center;
}

.key:active {
  transform: scale(0.98, 0.98) translateY(2px);
}
</style>
