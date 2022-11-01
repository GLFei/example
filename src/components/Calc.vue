<template>
  <div class="calc-panel">
    <div class="calc-result">
      <div class="equation">{{ equation }}</div>
      <div
        class="result"
        :class="[result.toString().length >= 8 ? 'long' : '']"
      >
        {{ calcResult }}
      </div>
    </div>
    <div class="calc-keyboard">
      <div
        class="button"
        :class="[item.cols == 2 ? 'double-button' : '', item.type]"
        v-for="(item, index) in buttonList"
        :key="index"
        @click="handleClick(item)"
      >
        {{ item.label }}
      </div>
    </div>
  </div>
</template>

<script>
// import Vue from 'vue';

export default {
  data() {
    return {
      buttonList: [
        { label: "AC", type: "operate", value: "clear" },
        { label: "±", type: "operate", value: "plus-minus" },
        { label: "%", type: "operate", value: "percent" },
        { label: "÷", type: "method" },
        { label: "7", type: "number" },
        { label: "8", type: "number" },
        { label: "9", type: "number" },
        { label: "×", type: "method" },
        { label: "4", type: "number" },
        { label: "5", type: "number" },
        { label: "6", type: "number" },
        { label: "-", type: "method" },
        { label: "1", type: "number" },
        { label: "2", type: "number" },
        { label: "3", type: "number" },
        { label: "+", type: "method" },
        { label: "0", type: "number", cols: 2 },
        { label: ".", type: "number" },
        { label: "=", type: "method", value: "eq" },
      ],
      equation: "",
      beforeInput: [],
      inputValue: ["0"],
      result: "0",

      isEq: false,
      method: "",
      isMethod: false,
    };
  },
  computed: {
    calcResult: function () {
      if (this.result.toString().length > 14) {
        return this.result.toString().slice(0, 14);
      } else {
        return this.result;
      }
    },
  },
  methods: {
    handleClick(item) {
      console.log(item);

      if (this.calcResult == "Infinity") {
        //   出错了只能清空
        if (item.value == "clear") {
          this.handleOperate(item);
        }
        return;
      }
      if (item.type === "number") {
        this.handleNumberInput(item);
      }

      if (item.type === "method") {
        if (item.value === "eq") {
          if (this.method) {
            let beforeValue = Number(this.beforeInput.join(""));
            let currentValue = Number(this.inputValue.join(""));
            switch (this.method) {
              case "+":
                this.result = beforeValue + currentValue;
                this.equation =
                  this.toSplit14(beforeValue) +
                  this.method +
                  currentValue +
                  "=";
                break;
              case "-":
                this.result = beforeValue - currentValue;
                this.equation =
                  this.toSplit14(beforeValue) +
                  this.method +
                  currentValue +
                  "=";
                break;
              case "×":
                this.result = beforeValue * currentValue;
                this.equation =
                  this.toSplit14(beforeValue) +
                  this.method +
                  currentValue +
                  "=";
                break;
              case "÷":
                this.result = beforeValue / currentValue;
                this.equation =
                  this.toSplit14(beforeValue) +
                  this.method +
                  currentValue +
                  "=";
                break;
            }
            this.beforeInput = this.result.toString().split("");
          } else {
            this.equation = this.toSplit14(this.result) + "=";
          }
          //   this.result = this.result;
          this.isEq = true;
        } else {
          this.handleMethod(item);
        }
      }

      if (item.type === "operate") {
        this.handleOperate(item);
      }
    },
    // 数值输入
    handleNumberInput(item) {
      // 已经计算过，清空结果和输入值
      if (this.isEq) {
        this.equation = "";
        this.inputValue = [item.label];
        this.isEq = false;
      } else if (this.isMethod) {
        this.isMethod = false;
        // 输入了计算方法
        if (item.label == ".") {
          this.inputValue = ["0", "."];
        } else {
          this.inputValue = [item.label];
        }
      } else {
        if (this.inputValue.length > 14) {
          return;
        }
        if (item.label == ".") {
          // 小数输入
          if (!this.inputValue.some((i) => i == item.label)) {
            this.inputValue.push(item.label);
          }
        } else if (this.inputValue.length == 1 && this.inputValue[0] == "0") {
          // 输入为0时,替换输入值
          this.inputValue = [item.label];
        } else {
          this.inputValue.push(item.label);
        }
      }
      this.result = this.inputValue.join("");
    },
    // 计算方法输入
    handleMethod(item) {
      if (this.isEq) {
        this.isEq = false;
        this.beforeInput = this.result.toString().split("");
      } else {
        this.beforeInput = JSON.parse(JSON.stringify(this.inputValue));
      }
      this.method = item.label;
      this.equation = this.beforeInput.join("") + item.label;
      this.isMethod = true;
    },
    // 其他操作
    handleOperate(item) {
      if (item.value == "clear") {
        this.isEq = false;
        this.isMethod = false;
        this.method = "";
        this.equation = "";
        this.beforeInput = [];
        this.inputValue = ["0"];
        this.result = "0";
      }
      if (item.value == "percent") {
        let res = Number(this.result);
        this.result = res / 100;
        this.inputValue = this.result.toString().split("");
      }
      if (item.value == "plus-minus") {
        let res = Number(this.result);
        this.result = res / -1;
        this.inputValue = this.result.toString().split("");
      }
    },

    // 最长显示14位数
    toSplit14(value) {
      let _value = value.toString();
      if (_value.length > 14) {
        return _value.slice(0, 14);
      } else {
        return _value;
      }
    },
  },
};
</script>

<style>
.calc-panel {
  display: flex;
  flex-direction: column;
  background-color: rgb(32, 29, 26);
  color: white;
  padding: 30px 10px 10px;
  width: 280px;
  border-radius: 8px;
  margin: 0 auto;
}

.calc-result {
  display: flex;
  flex-direction: column;
  text-align: right;
  padding: 0 10px;
}

.equation {
  height: 22px;
}
.result {
  font-size: 50px;
  height: 56px;
}

.long {
  font-size: 30px;
}

.calc-keyboard {
  display: flex;
  flex-wrap: wrap;
}
.calc-keyboard .button {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 60px;
  height: 60px;
  font-size: 20px;
  border-radius: 999px;
  background-color: #555555;
  margin: 5px;
}
.calc-keyboard .button:hover {
  background-color: #999999;
}

.calc-keyboard .double-button {
  width: 130px;
}

.calc-keyboard .button.operate {
  background-color: #888888;
}
.calc-keyboard .button.operate:hover {
  background-color: #aaaaaa;
}
.calc-keyboard .button.method {
  background-color: #2a7ce7;
}
.calc-keyboard .button.method:hover {
  background-color: #4f92eb;
}
</style>
