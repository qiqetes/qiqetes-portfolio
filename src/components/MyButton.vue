<template>
  <div style="display: inline-block;">
    <button v-on:click="onClick()">
      <div style="display: inline-block;">
        <div>
          <h2>
            <slot></slot>
            <i :class="i"></i>
          </h2>
        </div>
      </div>
    </button>
  </div>
</template>

<script>
export default {
  name: "MyButton",
  props: {
    i: String,
    onClick: Function
  }
};
</script>

<style lang="scss">
@mixin box-shadow($level) {
  @if $level == 1 {
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  } @else if $level == 2 {
    box-shadow: 0px 6px 20px rgba(0, 0, 0, 0.2);
  } @else if $level == 3 {
    box-shadow: 0px 10px 40px rgba(0, 0, 0, 0.3);
  } @else if $level == 4 {
    box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 40px rgba(0, 0, 0, 0.1);
  } @else if $level == 5 {
    box-shadow: 0 19px 38px rgba(0, 0, 0, 0.3), 0 15px 12px rgba(0, 0, 0, 0.22);
  }
}

button {
  margin: 12px;
  font-family: "Space Mono";
  background-color: white;
  border: 0;
  border-radius: 100px;
  min-width: 150px;
  @include box-shadow(2);
  color: #2c3e50;
  transition: box-shadow 0.5s;
}
button:focus {
  outline: 1px solid transparent;
  outline-offset: -4px;
}
button:hover {
  @include box-shadow(3);
}

button:active {
  transform: scale(0.99);
}
i {
  margin-left: 10px;
}
h2 {
  margin: 10px 15px 10px 15px;
}
</style>