<template>
  <div>
    <p v-if="string" :class="[message ? 'true' : 'false']">
      {{ string }}
    </p>

    <div v-if="string">
      <div class="message" v-if="message">Your string is balanced!</div>
      <div class="message" v-if="!message">Your string is not balanced!</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: null,
    };
  },
  props: {
    string: {
      type: String,
      default: null,
    },
  },
  watch: {
    string(newValue) {
      if (this.string.length > 0) {
        this.message = this.isStringBalanced(newValue);
      }
    },
  },
  methods: {
    isStringBalanced(string) {
      // Declaration of a stack to put the opening bracket
      let stack = [];

      // Going through each character
      for (let i = 0; i < string.length; i++) {
        if (string[i] == "(" || string[i] == "[" || string[i] == "{") {
          // Push the character in the stack
          stack.push(string[i]);
        }

        // At this moment, if the character is not opening bracket, that means it's a closing one so the stack cannot be empty at this point.
        if (stack.length == 0) return false;

        // If the current character is a closing bracket -> pop from stack
        // if the popped character is the matching starting bracket -> okay, if not -> brackets are not balanced.
        let check;
        switch (string[i]) {
          case ")":
            check = stack.pop();
            // if remaining stack is different that the one we popped -> false
            if (check == "{" || check == "[") return false;
            break;
          case "}":
            check = stack.pop();
            if (check == "(" || check == "[") return false;
            break;
          case "]":
            check = stack.pop();
            if (check == "(" || check == "{") return false;
            break;
        }
      }

      // if stack is empty -> it's balanced
      return stack.length == 0;
    },
  },
};
</script>

<style scoped>
p {
  display: block;
  width: 10%;
  padding: 20px 30px;
  text-align: center;
  margin: 20px;
  border-radius: 15px;
  font-size: 14px;
  cursor: pointer;
  margin: 0 auto;
}

.false {
  background-color: #f8d7da;
  color: #842029;
}

.true {
  color: #0f5132;
  background-color: #d1e7dd;
}

.message {
  margin: 20px;
}
</style>
